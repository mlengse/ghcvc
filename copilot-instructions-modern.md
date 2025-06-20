# SIMPUS Puskesmas - Custom Instructions Global

Gunakan bahasa Indonesia untuk semua interaksi. 
Gunakan tanggal hari ini dengan tepat.
Fokus pada pengembangan sistem informasi Puskesmas dengan keamanan, compliance, dan maintainability sebagai prioritas utama.

## Project Overview

**Domain:** Sistem Informasi Manajemen Puskesmas (Healthcare Information System)
SIMPUS adalah ecosystem aplikasi terintegrasi untuk manajemen operasional Puskesmas, meliputi:
- Manajemen pasien dan rekam medis
- Sistem antrian dan pendaftaran
- Integrasi BPJS Kesehatan dan Mobile JKN
- Laporan kesehatan dan monitoring
- Farmasi dan inventory obat

**Current Architecture:** Monolithic Legacy → Target: Microservices Modern Stack

## Technology Stack

**Legacy Systems (Maintenance Mode)**:
- j-care: CakePHP 1.3 (sistem utama Puskesmas) 
- antrian: CodeIgniter 2.x (sistem antrian)
- bpjsantrian: Pure PHP (integrasi BPJS antrian)
- siappkm_bpjs: Pure PHP (integrasi BPJS SIAP PKM)
- Database: MySQL 5.7+ (shared across all systems)

**Target Modern Stack (Migration Mode)**:
- Backend: Go 1.21+ (Gin/Echo framework)
- Frontend: Next.js 14+ (App Router, TypeScript)
- Database: MySQL 8.0+ (same schema, normalized)
- API: RESTful dengan OpenAPI/Swagger documentation
- Authentication: JWT/OAuth2 (migration dari session-based)

## Architecture Guidelines

### Legacy Maintenance (Current)
**Principle:** MINIMAL CHANGES - Maximum stability, essential security fixes only

**CakePHP 1.3 (j-care):**
- Maintain MVC structure: Model-Controller-View separation
- Use existing database.php untuk connections
- Follow CakePHP conventions: snake_case untuk database, camelCase untuk methods
- Implement security patches ONLY - no feature additions
- All database queries MUST use prepared statements

**CodeIgniter 2.x (antrian):**
- Maintain framework conventions: Controllers, Models, Views, Libraries
- Use Active Record untuk database operations
- Implement XSS filtering dan CSRF protection
- No breaking changes to existing API endpoints

**Pure PHP (bpjsantrian, siappkm_bpjs):**
- Maintain procedural programming style
- Add input validation dan output sanitization
- Use MySQLi prepared statements untuk security
- Preserve existing BPJS API integrations

### Modern Migration (Target)
**Principle:** CLEAN ARCHITECTURE - Layered separation with clear boundaries

**Go Backend Architecture:**
```
Domain Layer (Business entities dan rules)
├── Service Layer (Use cases dan business logic)
├── Interface Layer (HTTP handlers dan middleware)
├── Infrastructure Layer (Database, external APIs)
└── External Layer (BPJS, file system, third-party)
```

**Next.js Frontend Architecture:**
```
App Router Layer (Server Components, routing)
├── Feature Layer (Business components)
├── UI Layer (Reusable components)
└── Lib Layer (Utilities, API clients, hooks)
```

## Database Standards

**Schema Conventions:**
- Tables: snake_case naming (e.g., `finger_pasien`, `finger_unit`)
- Primary Keys: `id` (auto-increment integer)
- Foreign Keys: `{table}_id` format (e.g., `pasien_id`, `unit_id`)
- Timestamps: `created`, `updated` (datetime fields)
- Status Fields: ENUM atau VARCHAR dengan defined values
- Soft Deletes: `deleted_at` (nullable datetime)

**Critical Healthcare Tables:**
- `finger_pasien` - Master data pasien
- `finger_unit` - Unit layanan Puskesmas
- `finger_kunjungan` - Record kunjungan pasien
- `finger_obat` - Master obat dan inventory
- `finger_penyakit` - Master penyakit/ICD-10
- `finger_bpjs_*` - Tables untuk integrasi BPJS

**Migration Strategy:**
- Keep existing MySQL schema during transition
- Normalize data incrementally
- Maintain backward compatibility dengan legacy systems
- Use database versioning (migration scripts)

## Coding Standards

### Legacy PHP (Maintenance)
```php
// CakePHP 1.3 - Model example
class Patient extends AppModel {
    var $name = 'Patient';
    var $useTable = 'finger_pasien';
    
    // SECURITY: Always use parameterized queries
    function findByNIK($nik) {
        return $this->find('first', array(
            'conditions' => array('Patient.nik' => $nik)
        ));
    }
}

// CodeIgniter 2.x - Controller example  
class Antrian extends CI_Controller {
    public function add() {
        // SECURITY: Input validation
        $data = $this->input->post();
        $data = $this->security->xss_clean($data);
        
        if ($this->Antrian_model->insert($data)) {
            $this->output->set_output(json_encode(['status' => 'success']));
        }
    }
}
```

### Modern Go/Next.js (Target)
```go
// Go - Clean Architecture example
type PatientService struct {
    patientRepo domain.PatientRepository
    auditLogger domain.AuditLogger
}

func (s *PatientService) RegisterPatient(ctx context.Context, req RegisterPatientRequest) (*Patient, error) {
    // Business logic dengan proper validation
    patient := domain.NewPatient(req.Name, req.NIK)
    
    // Audit trail untuk healthcare compliance
    defer s.auditLogger.Log(ctx, "PATIENT_REGISTRATION", patient.ID)
    
    return s.patientRepo.Create(ctx, patient)
}
```

```typescript
// Next.js - Component example
export function PatientForm() {
  const form = useForm<PatientData>({
    resolver: zodResolver(patientSchema), // Type-safe validation
  })
  
  // ACCESSIBILITY: Proper labels and ARIA attributes
  return (
    <form onSubmit={form.handleSubmit(onSubmit)}>
      <label htmlFor="nik">NIK *</label>
      <input
        id="nik"
        {...form.register('nik')}
        aria-describedby="nik-error"
      />
    </form>
  )
}
```

## Security & Healthcare Compliance

**Data Privacy (Critical):**
- NIK dan data medis HARUS di-encrypt at rest
- Implement comprehensive audit trail
- Access control berbasis role (admin, dokter, perawat, operator)
- Session timeout untuk workstations
- HTTPS only untuk semua komunikasi

**BPJS Integration Security:**
- Store API credentials di environment variables
- Implement proper error handling untuk network failures
- Rate limiting untuk API calls
- Retry logic dengan exponential backoff
- Maintain sync integrity antara local dan BPJS data

**Healthcare Standards:**
- Patient consent management
- Data retention policies compliance
- Audit logs untuk semua akses data medis
- Backup dan disaster recovery procedures
- Medical device software guidelines compliance

## Testing Requirements

**Legacy Systems (Minimal):**
- Manual testing untuk security fixes
- Regression testing pada core workflows
- BPJS integration testing di staging environment

**Modern Systems (Comprehensive):**
- Unit tests: 80%+ coverage untuk business logic
- Integration tests: API endpoints dan database operations
- E2E tests: Critical user workflows (patient registration, queue management)
- Security tests: Penetration testing dan vulnerability scans
- Performance tests: Load testing untuk peak usage

## Documentation Standards

**Code Documentation:**
```php
/**
 * Register new patient dengan validasi NIK dan BPJS
 * 
 * @param array $data Patient data from form
 * @return array|false Patient record atau false jika gagal
 * @throws InvalidArgumentException Jika NIK format salah
 * @security Input di-sanitize sebelum database operation
 */
function registerPatient($data) {
    // Implementation
}
```

**API Documentation:**
- OpenAPI/Swagger untuk semua modern endpoints
- Include examples dan error codes
- Healthcare-specific field descriptions
- Security requirements per endpoint

**Database Documentation:**
- ER diagrams untuk complex relationships
- Data dictionary dengan healthcare terminology
- Migration scripts dengan rollback procedures
- Index optimization documentation

## Integration Guidance

**Chat Modes:** Gunakan chat mode yang sesuai untuk setiap task:
- `legacy-php-maintenance.chatmode.md` - Untuk maintenance PHP legacy
- `modernization-architect.chatmode.md` - Untuk planning migration strategy
- `development.chatmode.md` - Untuk implementasi features baru

**Prompts:** Gunakan custom prompts untuk tasks berulang:
- `legacy-migration-analysis.prompt.md` - Untuk analisis migration planning
- `create-custom-chatmode.prompt.md` - Untuk membuat chat modes baru

**Instructions:** Language-specific instructions:
- `clean-architecture-go.instructions.md` - Go backend development
- `component-architecture-nextjs.instructions.md` - Next.js frontend development
- `legacy-maintenance.instructions.md` - PHP legacy maintenance

## Quality Assurance Standards

**Performance Targets:**
- API response time: < 200ms untuk CRUD operations
- Page load time: < 3 seconds pada koneksi 3G
- Database queries: < 100ms untuk single record retrieval
- Memory usage: < 512MB per request pada peak load

**Availability Requirements:**
- Uptime: 99.5% (maximum 36 hours downtime per year)
- Recovery time: < 4 hours untuk critical system failures
- Backup frequency: Daily automated backups dengan 30-day retention
- Disaster recovery: < 24 hours untuk full system restoration

**Medical Software Compliance:**
- Patient safety: Zero tolerance untuk data corruption
- Audit compliance: Complete audit trail dengan tamper-proof logging
- Access control: Role-based permissions dengan principle of least privilege
- Data integrity: Checksums dan validation untuk critical medical data

Selalu prioritaskan keamanan data medis, compliance dengan standar healthcare, dan stability sistem dalam segala pengembangan code.
