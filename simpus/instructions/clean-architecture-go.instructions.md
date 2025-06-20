---
applies_to: "**/*.go"
description: "Clean Architecture instructions for SIMPUS Go backend development"
---

# Clean Architecture Instructions - SIMPUS Go Backend

## Architecture Overview

Clean Architecture adalah pola arsitektur yang memisahkan kode menjadi layer-layer dengan tanggung jawab yang jelas dan dependency direction yang konsisten. Dalam konteks SIMPUS Go backend, arsitektur ini memastikan:

- **Independence**: Business logic tidak bergantung pada framework, database, atau UI
- **Testability**: Setiap layer dapat ditest secara independen
- **Maintainability**: Perubahan pada satu layer tidak mempengaruhi layer lain
- **Healthcare Compliance**: Audit trail dan security dapat diimplementasikan di layer yang tepat

```
┌─────────────────────────────────────┐
│           External Layer            │  
│  (Database, BPJS API, File System)  │
├─────────────────────────────────────┤
│         Infrastructure Layer        │
│   (Repositories, HTTP Clients)      │
├─────────────────────────────────────┤
│          Interface Layer            │
│      (Handlers, Middleware)         │
├─────────────────────────────────────┤
│           Service Layer             │
│      (Business Logic, Use Cases)    │
├─────────────────────────────────────┤
│           Domain Layer              │
│       (Entities, Domain Rules)      │
└─────────────────────────────────────┘
```

## Layer-Specific Guidelines

### 1. Domain Layer (`internal/domain/`)

**Tanggung Jawab:**
- Mendefinisikan core business entities (Patient, Queue, Appointment)
- Business rules dan domain logic
- Domain events untuk audit trail
- Value objects dan aggregates

**Structure:**
```go
// internal/domain/patient.go
type Patient struct {
    ID         uint   `json:"id"`
    NoRM       string `json:"no_rm" validate:"required"`
    NIK        string `json:"nik" validate:"required,len=16"`
    Name       string `json:"name" validate:"required,min=2"`
    BPJSNumber string `json:"bpjs_number,omitempty"`
    // ... other fields
}

// Domain methods
func (p *Patient) IsEligibleForBPJS() bool {
    return p.BPJSNumber != ""
}

func (p *Patient) GenerateAuditEvent(action string) AuditEvent {
    return AuditEvent{
        EntityType: "Patient",
        EntityID:   p.ID,
        Action:     action,
        Timestamp:  time.Now(),
    }
}
```

**Rules:**
- NO dependencies pada layer lain
- Pure Go structs dan methods
- Business validation logic hanya disini
- Immutable ketika memungkinkan

### 2. Service Layer (`internal/service/`)

**Tanggung Jawab:**
- Orchestrate business use cases
- Koordinasi antar domain entities
- Transaction management
- Business workflow implementation

**Structure:**
```go
// internal/service/patient_service.go
type PatientService struct {
    patientRepo domain.PatientRepository
    auditRepo   domain.AuditRepository
    bpjsClient  domain.BPJSClient
    logger      domain.Logger
}

func (s *PatientService) RegisterPatient(ctx context.Context, req RegisterPatientRequest) (*domain.Patient, error) {
    // 1. Validate business rules
    if err := s.validatePatientRegistration(req); err != nil {
        return nil, err
    }
    
    // 2. Create domain entity
    patient := domain.NewPatient(req.Name, req.NIK, req.BPJSNumber)
    
    // 3. Check BPJS eligibility if needed
    if patient.HasBPJS() {
        if err := s.verifyBPJSEligibility(ctx, patient); err != nil {
            return nil, err
        }
    }
    
    // 4. Save to repository
    savedPatient, err := s.patientRepo.Create(ctx, patient)
    if err != nil {
        return nil, err
    }
    
    // 5. Create audit trail
    auditEvent := patient.GenerateAuditEvent("CREATE")
    s.auditRepo.Log(ctx, auditEvent)
    
    return savedPatient, nil
}
```

**Rules:**
- Hanya bergantung pada domain interfaces
- Implement transaction boundaries
- Error handling dengan proper context
- Logging untuk audit dan debugging

### 3. Interface Layer (`internal/handler/`)

**Tanggung Jawab:**
- HTTP request/response handling
- Input validation dan sanitization
- Response formatting
- Authentication/authorization

**Structure:**
```go
// internal/handler/patient_handler.go
type PatientHandler struct {
    patientService service.PatientService
    validator      *validator.Validate
}

func (h *PatientHandler) CreatePatient(c *gin.Context) {
    var req CreatePatientRequest
    
    // 1. Bind and validate request
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, ErrorResponse{
            Code:    "INVALID_REQUEST",
            Message: "Invalid request format",
            Details: err.Error(),
        })
        return
    }
    
    if err := h.validator.Struct(req); err != nil {
        c.JSON(http.StatusBadRequest, ValidationErrorResponse{
            Code:   "VALIDATION_ERROR",
            Errors: formatValidationErrors(err),
        })
        return
    }
    
    // 2. Extract user context for audit
    userID := c.GetUint("user_id")
    ctx := context.WithValue(c.Request.Context(), "user_id", userID)
    
    // 3. Call service
    patient, err := h.patientService.RegisterPatient(ctx, service.RegisterPatientRequest{
        Name:       req.Name,
        NIK:        req.NIK,
        BPJSNumber: req.BPJSNumber,
    })
    
    if err != nil {
        h.handleServiceError(c, err)
        return
    }
    
    // 4. Return response
    c.JSON(http.StatusCreated, SuccessResponse{
        Code: "PATIENT_CREATED",
        Data: PatientResponse{
            ID:         patient.ID,
            NoRM:       patient.NoRM,
            Name:       patient.Name,
            NIK:        patient.NIK,
            BPJSNumber: patient.BPJSNumber,
        },
    })
}
```

**Rules:**
- Tidak ada business logic disini
- Semua input harus divalidasi
- Consistent error response format
- Proper HTTP status codes

### 4. Infrastructure Layer (`internal/infrastructure/`)

**Tanggung Jawab:**
- Database implementation
- External API clients
- File system operations
- Third-party integrations

**Structure:**
```go
// internal/infrastructure/repository/patient_repository.go
type PatientRepository struct {
    db *gorm.DB
}

func (r *PatientRepository) Create(ctx context.Context, patient *domain.Patient) (*domain.Patient, error) {
    // Convert domain to database model
    dbPatient := &models.Patient{
        NoRM:       patient.NoRM,
        NIK:        patient.NIK,
        Name:       patient.Name,
        BPJSNumber: patient.BPJSNumber,
    }
    
    err := r.db.WithContext(ctx).Create(dbPatient).Error
    if err != nil {
        if isDuplicateError(err) {
            return nil, domain.ErrPatientAlreadyExists
        }
        return nil, fmt.Errorf("failed to create patient: %w", err)
    }
    
    // Convert back to domain
    return &domain.Patient{
        ID:         dbPatient.ID,
        NoRM:       dbPatient.NoRM,
        NIK:        dbPatient.NIK,
        Name:       dbPatient.Name,
        BPJSNumber: dbPatient.BPJSNumber,
    }, nil
}

// internal/infrastructure/client/bpjs_client.go
type BPJSClient struct {
    baseURL    string
    httpClient *http.Client
    userKey    string
    secretKey  string
}

func (c *BPJSClient) VerifyParticipant(ctx context.Context, bpjsNumber string) (*domain.BPJSParticipant, error) {
    // Implementation for BPJS API call
    // Include proper error handling and retry logic
}
```

**Rules:**
- Implement domain interfaces
- Handle external errors gracefully
- Database transactions untuk consistency
- Proper connection management

## Cross-Layer Communication Rules

### Dependency Direction
```go
// ✅ CORRECT: Dependencies point inward
Handler -> Service -> Domain
Infrastructure -> Domain (implements interfaces)

// ❌ WRONG: Dependencies pointing outward  
Domain -> Infrastructure
Service -> Handler
```

### Interface Usage
```go
// Domain defines interfaces
type PatientRepository interface {
    Create(ctx context.Context, patient *Patient) (*Patient, error)
    GetByID(ctx context.Context, id uint) (*Patient, error)
    GetByNIK(ctx context.Context, nik string) (*Patient, error)
}

// Infrastructure implements
type PatientRepository struct {
    db *gorm.DB
}

// Service uses interface
type PatientService struct {
    patientRepo domain.PatientRepository // interface, not concrete type
}
```

### Data Transfer Patterns
```go
// Use specific request/response types for each layer
type CreatePatientRequest struct {    // Handler layer
    Name       string `json:"name" validate:"required"`
    NIK        string `json:"nik" validate:"required,len=16"`
    BPJSNumber string `json:"bpjs_number,omitempty"`
}

type RegisterPatientRequest struct {  // Service layer
    Name       string
    NIK        string
    BPJSNumber string
    CreatedBy  uint
}

type Patient struct {               // Domain layer
    ID         uint
    NoRM       string
    NIK        string
    Name       string
    BPJSNumber string
}
```

## Testing Approach

### Domain Layer Testing
```go
func TestPatient_IsEligibleForBPJS(t *testing.T) {
    tests := []struct {
        name       string
        patient    *domain.Patient
        expected   bool
    }{
        {
            name: "patient with BPJS number is eligible",
            patient: &domain.Patient{
                BPJSNumber: "0001234567890",
            },
            expected: true,
        },
        {
            name: "patient without BPJS number is not eligible",
            patient: &domain.Patient{
                BPJSNumber: "",
            },
            expected: false,
        },
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            result := tt.patient.IsEligibleForBPJS()
            assert.Equal(t, tt.expected, result)
        })
    }
}
```

### Service Layer Testing
```go
func TestPatientService_RegisterPatient(t *testing.T) {
    // Setup mocks
    mockPatientRepo := mocks.NewPatientRepository(t)
    mockAuditRepo := mocks.NewAuditRepository(t)
    mockBPJSClient := mocks.NewBPJSClient(t)
    
    service := service.NewPatientService(
        mockPatientRepo,
        mockAuditRepo,
        mockBPJSClient,
        logger,
    )
    
    // Test implementation with mocks
    mockPatientRepo.EXPECT().Create(mock.Anything, mock.Anything).
        Return(&domain.Patient{ID: 1}, nil)
    
    // Execute test
    result, err := service.RegisterPatient(ctx, req)
    
    // Assertions
    assert.NoError(t, err)
    assert.NotNil(t, result)
}
```

### Handler Layer Testing
```go
func TestPatientHandler_CreatePatient(t *testing.T) {
    // Setup
    mockService := mocks.NewPatientService(t)
    handler := handler.NewPatientHandler(mockService, validator)
    
    // Setup HTTP test
    gin.SetMode(gin.TestMode)
    router := gin.New()
    router.POST("/patients", handler.CreatePatient)
    
    // Test request
    body := `{"name":"John Doe","nik":"1234567890123456"}`
    req := httptest.NewRequest("POST", "/patients", strings.NewReader(body))
    req.Header.Set("Content-Type", "application/json")
    
    w := httptest.NewRecorder()
    router.ServeHTTP(w, req)
    
    // Assertions
    assert.Equal(t, http.StatusCreated, w.Code)
}
```

## Common Anti-patterns to Avoid

### 1. ❌ Business Logic in Handlers
```go
// DON'T DO THIS
func (h *PatientHandler) CreatePatient(c *gin.Context) {
    // Business logic in handler - WRONG!
    if req.NIK == "" || len(req.NIK) != 16 {
        c.JSON(400, gin.H{"error": "Invalid NIK"})
        return
    }
    
    // Direct database access from handler - WRONG!
    err := h.db.Create(&patient).Error
}
```

### 2. ❌ Domain Layer Dependencies
```go
// DON'T DO THIS
package domain

import "gorm.io/gorm" // External dependency in domain - WRONG!

type Patient struct {
    gorm.Model // Framework coupling in domain - WRONG!
    Name string
}
```

### 3. ❌ Service Layer HTTP Concerns
```go
// DON'T DO THIS
func (s *PatientService) CreatePatient(c *gin.Context) error {
    // HTTP context in service - WRONG!
    var req CreatePatientRequest
    c.ShouldBindJSON(&req) // Handler concern in service - WRONG!
}
```

### 4. ❌ Infrastructure in Business Logic
```go
// DON'T DO THIS
func (s *PatientService) RegisterPatient(req RegisterPatientRequest) error {
    // Direct database access in service - WRONG!
    err := s.db.Create(&patient).Error
    
    // Direct HTTP client usage - WRONG!
    resp, err := http.Get("https://bpjs-api.com/verify")
}
```

## Healthcare-Specific Considerations

### Audit Trail Implementation
```go
// Domain layer defines audit requirements
type AuditEvent struct {
    EntityType string
    EntityID   uint
    Action     string
    UserID     uint
    Timestamp  time.Time
    Changes    map[string]interface{}
}

// Service layer orchestrates audit logging
func (s *PatientService) UpdatePatient(ctx context.Context, id uint, req UpdatePatientRequest) error {
    oldPatient, _ := s.patientRepo.GetByID(ctx, id)
    
    // Update patient...
    
    // Create audit trail
    changes := calculateChanges(oldPatient, updatedPatient)
    auditEvent := AuditEvent{
        EntityType: "Patient",
        EntityID:   id,
        Action:     "UPDATE",
        UserID:     getUserIDFromContext(ctx),
        Timestamp:  time.Now(),
        Changes:    changes,
    }
    
    s.auditRepo.Log(ctx, auditEvent)
}
```

### Data Privacy & Security
```go
// Domain layer defines sensitive data
type Patient struct {
    ID         uint   `json:"id"`
    NIK        string `json:"-"` // Never serialize NIK
    Name       string `json:"name"`
    // ... other fields
}

// Service layer handles encryption
func (s *PatientService) CreatePatient(ctx context.Context, req CreatePatientRequest) error {
    // Encrypt sensitive data before storage
    encryptedNIK, err := s.encryptor.Encrypt(req.NIK)
    if err != nil {
        return err
    }
    
    patient := &domain.Patient{
        NIK:  encryptedNIK,
        Name: req.Name,
    }
    
    return s.patientRepo.Create(ctx, patient)
}
```

## Implementation Guidelines

### Project Structure
```
cmd/
├── api/
│   └── main.go
internal/
├── domain/          # Business entities and rules
│   ├── patient.go
│   ├── queue.go
│   └── interfaces.go
├── service/         # Use cases and business logic
│   ├── patient_service.go
│   └── queue_service.go
├── handler/         # HTTP handlers
│   ├── patient_handler.go
│   └── queue_handler.go
├── infrastructure/  # External concerns
│   ├── repository/
│   ├── client/
│   └── middleware/
└── config/          # Configuration
    └── config.go
```

### Dependency Injection Setup
```go
// cmd/api/main.go
func main() {
    // Infrastructure setup
    db := setupDatabase()
    bpjsClient := setupBPJSClient()
    
    // Repository layer
    patientRepo := repository.NewPatientRepository(db)
    auditRepo := repository.NewAuditRepository(db)
    
    // Service layer
    patientService := service.NewPatientService(
        patientRepo,
        auditRepo,
        bpjsClient,
        logger,
    )
    
    // Handler layer
    patientHandler := handler.NewPatientHandler(patientService, validator)
    
    // Route setup
    router := setupRoutes(patientHandler)
    router.Run(":8080")
}
```

### Error Handling Strategy
```go
// Domain layer defines business errors
var (
    ErrPatientNotFound     = errors.New("patient not found")
    ErrPatientAlreadyExists = errors.New("patient already exists")
    ErrInvalidBPJSNumber   = errors.New("invalid BPJS number")
)

// Service layer handles and wraps errors
func (s *PatientService) GetPatient(ctx context.Context, id uint) (*domain.Patient, error) {
    patient, err := s.patientRepo.GetByID(ctx, id)
    if err != nil {
        if errors.Is(err, domain.ErrPatientNotFound) {
            return nil, err // Pass through domain errors
        }
        return nil, fmt.Errorf("failed to get patient: %w", err)
    }
    return patient, nil
}

// Handler layer maps errors to HTTP responses
func (h *PatientHandler) handleServiceError(c *gin.Context, err error) {
    switch {
    case errors.Is(err, domain.ErrPatientNotFound):
        c.JSON(http.StatusNotFound, ErrorResponse{
            Code:    "PATIENT_NOT_FOUND",
            Message: "Patient not found",
        })
    case errors.Is(err, domain.ErrPatientAlreadyExists):
        c.JSON(http.StatusConflict, ErrorResponse{
            Code:    "PATIENT_EXISTS",
            Message: "Patient already exists",
        })
    default:
        c.JSON(http.StatusInternalServerError, ErrorResponse{
            Code:    "INTERNAL_ERROR",
            Message: "Internal server error",
        })
    }
}
```

Ikuti instruksi ini secara konsisten untuk memastikan kode Go backend SIMPUS mengikuti Clean Architecture principles dan dapat di-maintain dengan baik selama proses modernisasi.
