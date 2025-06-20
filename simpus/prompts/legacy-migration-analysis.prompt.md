---
mode: "ask"
description: "Analyze legacy PHP modules and generate comprehensive migration plan to Go backend + Next.js frontend"
---

# Legacy to Modern Migration Analysis

## Migration Target Analysis

Analyze the selected legacy PHP module(s) and create a comprehensive migration plan to Go backend + Next.js frontend while maintaining the existing MySQL database.

### Module Information
- **Legacy Module**: [Specify: j-care, antrian, bpjsantrian, or siappkm_bpjs]
- **Framework**: [Auto-detect: CakePHP 1.3, CodeIgniter 2.x, or Pure PHP]
- **Primary Functions**: [Brief description of module's main purpose]

## Analysis Requirements

### 1. Database Schema Analysis
Examine the database structure used by this module:

```sql
-- Identify and document:
- Primary tables used by this module
- Foreign key relationships
- Indexes and constraints
- Data types and their Go/Next.js equivalents
- Potential schema improvements needed
```

### 2. API Endpoint Mapping
Document all HTTP endpoints in this module:

```php
// For each endpoint, document:
- Route pattern and HTTP method
- Controller and action method
- Input parameters (GET, POST, files)
- Response format (HTML, JSON, XML)
- Authentication/authorization requirements
- External API integrations (BPJS, etc.)
```

### 3. Business Logic Extraction
Identify core business rules and workflows:

```php
// Extract and document:
- Data validation rules
- Business calculations and logic
- Workflow sequences
- Integration points with other modules
- Critical error handling patterns
```

### 4. Frontend Components Analysis
Analyze UI components and user interactions:

```html
<!-- Document:
- Form structures and validation
- Data tables and pagination
- AJAX interactions
- File upload/download features
- Print functionality
- Real-time updates (if any)
-->
```

## Migration Strategy Design

### Phase 1: Foundation Setup
**Go Backend Setup:**
```go
// Recommended project structure:
cmd/
├── api/
│   └── main.go
internal/
├── handlers/
├── services/
├── repositories/
├── models/
└── middleware/
pkg/
├── database/
├── auth/
└── utils/
```

**Database Migration:**
```go
// GORM AutoMigrate or golang-migrate scripts
- Create migration files for schema normalization
- Data migration scripts if needed
- Backup and rollback procedures
```

### Phase 2: API Development
**RESTful API Design:**
```go
// For each legacy endpoint, create:
type [Entity]Handler struct {
    service [Entity]Service
}

func (h *[Entity]Handler) Create(c *gin.Context) {
    // Implementation with proper validation
}

// Include:
- Input validation with go-playground/validator
- Error handling with consistent response format
- Authentication middleware
- Rate limiting for sensitive endpoints
```

### Phase 3: Frontend Migration
**Next.js App Structure:**
```typescript
// Recommended structure:
app/
├── (dashboard)/
│   ├── patients/
│   ├── queue/
│   └── reports/
components/
├── ui/           // shadcn/ui components
├── forms/        // Medical forms
└── tables/       // Data tables
lib/
├── auth.ts
├── api.ts
└── validations.ts
```

**Component Migration Priority:**
1. Authentication and session management
2. Patient registration forms
3. Queue management interface
4. Reports and data tables
5. BPJS integration interfaces

### Phase 4: Integration & Testing
**Testing Strategy:**
```go
// Backend testing:
- Unit tests for business logic
- Integration tests for API endpoints
- Database transaction tests
- BPJS integration tests
```

```typescript
// Frontend testing:
- Component tests with React Testing Library
- Form validation tests
- API integration tests
- E2E tests for critical workflows
```

## Risk Assessment & Mitigation

### High-Risk Areas
- **Data Migration**: Patient data integrity during schema changes
- **BPJS Integration**: API compatibility during transition
- **Authentication**: Session management changes
- **File Handling**: Document and image uploads
- **Real-time Features**: Queue updates and notifications

### Mitigation Strategies
- **Parallel Deployment**: Run legacy and modern systems side-by-side
- **Gradual Rollout**: Module-by-module migration
- **Data Synchronization**: Bidirectional sync during transition
- **Rollback Plan**: Quick revert procedures for each phase

## Implementation Timeline

### Week 1-2: Analysis & Setup
- [ ] Complete database schema analysis
- [ ] Set up Go project structure
- [ ] Configure development environment
- [ ] Create initial migration scripts

### Week 3-4: Core API Development
- [ ] Implement authentication system
- [ ] Create core CRUD operations
- [ ] Set up middleware and error handling
- [ ] Write unit tests

### Week 5-6: Frontend Foundation
- [ ] Set up Next.js project
- [ ] Create UI component library
- [ ] Implement authentication flow
- [ ] Build core layouts

### Week 7-8: Feature Migration
- [ ] Migrate high-priority features
- [ ] Implement data tables and forms
- [ ] Set up API integration
- [ ] Add form validations

### Week 9-10: Integration & Testing
- [ ] BPJS API integration
- [ ] End-to-end testing
- [ ] Performance optimization
- [ ] Documentation updates

### Week 11-12: Deployment & Monitoring
- [ ] Production deployment setup
- [ ] Monitoring and logging
- [ ] Data migration execution
- [ ] Legacy system deprecation plan

## Quality Checklist

### Security Requirements
- [ ] Input validation on all endpoints
- [ ] SQL injection prevention
- [ ] XSS protection in frontend
- [ ] CSRF tokens implementation
- [ ] Proper authentication and authorization
- [ ] Data encryption for sensitive information

### Performance Standards
- [ ] API response time < 200ms
- [ ] Database query optimization
- [ ] Frontend bundle size optimization
- [ ] Lazy loading implementation
- [ ] Caching strategy implementation

### Healthcare Compliance
- [ ] Patient data privacy protection
- [ ] Audit trail implementation
- [ ] Data backup and recovery procedures
- [ ] HIPAA-equivalent compliance measures
- [ ] Access control implementation

## Documentation Requirements

### Technical Documentation
- [ ] API documentation with OpenAPI/Swagger
- [ ] Database schema documentation
- [ ] Deployment procedures
- [ ] Monitoring and maintenance guides

### User Documentation
- [ ] Migration impact for end users
- [ ] Training materials for new interface
- [ ] Troubleshooting guides
- [ ] Rollback procedures

## Success Metrics

### Performance Metrics
- [ ] 50% reduction in page load times
- [ ] 90% uptime during migration
- [ ] Zero data loss during migration
- [ ] 80% test coverage for new code

### User Experience Metrics
- [ ] Reduced training time for new interface
- [ ] Improved mobile usability
- [ ] Better accessibility compliance
- [ ] Faster workflow completion times

## Next Steps

Based on this analysis, the immediate next steps are:

1. **[Priority 1]**: Begin with database schema analysis and normalization
2. **[Priority 2]**: Set up Go backend project structure
3. **[Priority 3]**: Create API endpoint mapping documentation
4. **[Priority 4]**: Design Next.js component architecture
5. **[Priority 5]**: Develop migration timeline and resource allocation

## Usage Instructions

1. **Select the legacy module** you want to analyze using `#selection` or `#file`
2. **Run this prompt** to get comprehensive migration analysis
3. **Customize the analysis** based on specific module requirements
4. **Use with modernization-architect.chatmode.md** for detailed implementation guidance
5. **Update the analysis** as you discover new requirements during development

This prompt is designed to be used iteratively - run it for each major module or when significant changes are discovered during the migration process.
