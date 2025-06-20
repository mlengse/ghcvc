---
applies_to: "**/*.{ts,tsx,js,jsx}"
description: "Component Architecture instructions for SIMPUS Next.js frontend development"
---

# Component Architecture Instructions - SIMPUS Next.js Frontend

## Architecture Overview

Arsitektur frontend SIMPUS menggunakan **Component-Driven Development** dengan **Server Components First** approach untuk healthcare applications. Pattern ini memastikan:

- **Performance**: Optimal loading dengan Server Components
- **Accessibility**: WCAG 2.1 compliance untuk healthcare applications
- **Security**: Proper data handling untuk informasi medis
- **Maintainability**: Reusable components untuk medical forms dan data tables
- **User Experience**: Intuitive interfaces untuk staff Puskesmas

```
┌─────────────────────────────────────┐
│              App Router             │
│         (Route Handlers)            │
├─────────────────────────────────────┤
│             Page Layer              │
│      (Server Components)            │
├─────────────────────────────────────┤
│           Feature Layer             │
│    (Business Components)            │
├─────────────────────────────────────┤
│              UI Layer               │
│      (Reusable Components)          │
├─────────────────────────────────────┤
│             Lib Layer               │
│    (Utils, Hooks, Validations)      │
└─────────────────────────────────────┘
```

## Layer-Specific Guidelines

### 1. App Layer (`app/`)

**Tanggung Jawab:**
- Route definitions dan layout
- Server Components untuk data fetching
- Metadata dan SEO optimization
- Error boundaries dan loading states

**Structure:**
```typescript
// app/(dashboard)/patients/page.tsx
import { Metadata } from 'next'
import { PatientList } from '@/components/features/patient/patient-list'
import { getPatients } from '@/lib/api/patients'

export const metadata: Metadata = {
  title: 'Daftar Pasien - SIMPUS',
  description: 'Manajemen data pasien Puskesmas',
}

export default async function PatientsPage({
  searchParams,
}: {
  searchParams: { search?: string; page?: string }
}) {
  // Server-side data fetching
  const patients = await getPatients({
    search: searchParams.search,
    page: parseInt(searchParams.page || '1'),
  })

  return (
    <div className="container mx-auto py-6">
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-2xl font-bold">Daftar Pasien</h1>
      </div>
      
      <PatientList 
        patients={patients.data}
        pagination={patients.pagination}
      />
    </div>
  )
}
```

**Rules:**
- Gunakan Server Components secara default
- Client Components hanya untuk interactivity
- Proper metadata untuk setiap page
- Error handling dengan error.tsx

### 2. Feature Layer (`components/features/`)

**Tanggung Jawab:**
- Business-specific components
- Form handling dan validation
- State management untuk features
- Integration dengan backend APIs

**Structure:**
```typescript
// components/features/patient/patient-form.tsx
'use client'

import { useState } from 'react'
import { useRouter } from 'next/navigation'
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { createPatient } from '@/lib/api/patients'
import { patientSchema, type PatientFormData } from '@/lib/validations/patient'
import { useToast } from '@/hooks/use-toast'

export function PatientForm() {
  const [isLoading, setIsLoading] = useState(false)
  const router = useRouter()
  const { toast } = useToast()
  
  const form = useForm<PatientFormData>({
    resolver: zodResolver(patientSchema),
    defaultValues: {
      name: '',
      nik: '',
      phone: '',
      address: '',
      bpjsNumber: '',
    },
  })

  const onSubmit = async (data: PatientFormData) => {
    setIsLoading(true)
    
    try {
      await createPatient(data)
      
      toast({
        title: 'Berhasil',
        description: 'Data pasien berhasil disimpan',
      })
      
      router.push('/patients')
      router.refresh()
    } catch (error) {
      toast({
        title: 'Error',
        description: 'Gagal menyimpan data pasien',
        variant: 'destructive',
      })
    } finally {
      setIsLoading(false)
    }
  }

  return (
    <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-6">
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div className="space-y-2">
          <label htmlFor="name" className="text-sm font-medium">
            Nama Lengkap *
          </label>
          <Input
            id="name"
            {...form.register('name')}
            placeholder="Masukkan nama lengkap"
            aria-describedby="name-error"
          />
          {form.formState.errors.name && (
            <p id="name-error" className="text-sm text-red-600" role="alert">
              {form.formState.errors.name.message}
            </p>
          )}
        </div>

        <div className="space-y-2">
          <label htmlFor="nik" className="text-sm font-medium">
            NIK *
          </label>
          <Input
            id="nik"
            {...form.register('nik')}
            placeholder="16 digit NIK"
            maxLength={16}
            aria-describedby="nik-error"
          />
          {form.formState.errors.nik && (
            <p id="nik-error" className="text-sm text-red-600" role="alert">
              {form.formState.errors.nik.message}
            </p>
          )}
        </div>
      </div>

      <Button type="submit" disabled={isLoading} className="w-full">
        {isLoading ? 'Menyimpan...' : 'Simpan Data Pasien'}
      </Button>
    </form>
  )
}
```

**Rules:**
- One feature per directory
- Use React Hook Form + Zod untuk forms
- Proper error handling dan loading states
- Accessibility attributes (aria-*, role)

### 3. UI Layer (`components/ui/`)

**Tanggung Jawab:**
- Reusable UI components
- Design system implementation
- Accessibility standards
- Component variants dan composition

**Structure:**
```typescript
// components/ui/data-table.tsx
'use client'

import { useState } from 'react'
import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
} from '@/components/ui/table'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { cn } from '@/lib/utils'

interface Column<T> {
  key: keyof T
  label: string
  sortable?: boolean
  render?: (item: T) => React.ReactNode
}

interface DataTableProps<T> {
  data: T[]
  columns: Column<T>[]
  searchable?: boolean
  searchPlaceholder?: string
  onRowClick?: (item: T) => void
  className?: string
}

export function DataTable<T extends Record<string, any>>({
  data,
  columns,
  searchable = false,
  searchPlaceholder = 'Cari...',
  onRowClick,
  className,
}: DataTableProps<T>) {
  const [searchTerm, setSearchTerm] = useState('')
  const [sortColumn, setSortColumn] = useState<keyof T | null>(null)
  const [sortDirection, setSortDirection] = useState<'asc' | 'desc'>('asc')

  const filteredData = data.filter((item) =>
    Object.values(item).some((value) =>
      String(value).toLowerCase().includes(searchTerm.toLowerCase())
    )
  )

  const sortedData = sortColumn
    ? [...filteredData].sort((a, b) => {
        const aVal = a[sortColumn]
        const bVal = b[sortColumn]
        
        if (sortDirection === 'asc') {
          return aVal > bVal ? 1 : -1
        }
        return aVal < bVal ? 1 : -1
      })
    : filteredData

  return (
    <div className={cn('space-y-4', className)}>
      {searchable && (
        <div className="flex items-center space-x-2">
          <Input
            placeholder={searchPlaceholder}
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
            className="max-w-sm"
            aria-label="Pencarian data"
          />
        </div>
      )}

      <div className="rounded-md border">
        <Table>
          <TableHeader>
            <TableRow>
              {columns.map((column) => (
                <TableHead
                  key={String(column.key)}
                  className={cn(
                    column.sortable && 'cursor-pointer hover:bg-muted/50'
                  )}
                  onClick={() => {
                    if (column.sortable) {
                      if (sortColumn === column.key) {
                        setSortDirection(sortDirection === 'asc' ? 'desc' : 'asc')
                      } else {
                        setSortColumn(column.key)
                        setSortDirection('asc')
                      }
                    }
                  }}
                >
                  {column.label}
                  {column.sortable && sortColumn === column.key && (
                    <span className="ml-1">
                      {sortDirection === 'asc' ? '↑' : '↓'}
                    </span>
                  )}
                </TableHead>
              ))}
            </TableRow>
          </TableHeader>
          <TableBody>
            {sortedData.map((item, index) => (
              <TableRow
                key={index}
                className={cn(
                  onRowClick && 'cursor-pointer hover:bg-muted/50'
                )}
                onClick={() => onRowClick?.(item)}
              >
                {columns.map((column) => (
                  <TableCell key={String(column.key)}>
                    {column.render
                      ? column.render(item)
                      : String(item[column.key])}
                  </TableCell>
                ))}
              </TableRow>
            ))}
          </TableBody>
        </Table>
      </div>

      {sortedData.length === 0 && (
        <div className="text-center py-8 text-muted-foreground">
          Tidak ada data yang ditemukan
        </div>
      )}
    </div>
  )
}
```

**Rules:**
- Menggunakan shadcn/ui sebagai base
- Generic components dengan TypeScript
- Full accessibility support
- Composition over inheritance

### 4. Lib Layer (`lib/`)

**Tanggung Jawab:**
- API client functions
- Validation schemas
- Utility functions
- Custom hooks

**Structure:**
```typescript
// lib/api/patients.ts
import { apiClient } from './client'
import type { Patient, CreatePatientRequest, PaginatedResponse } from '@/types/patient'

export async function getPatients(params: {
  search?: string
  page?: number
  limit?: number
}): Promise<PaginatedResponse<Patient>> {
  const searchParams = new URLSearchParams()
  
  if (params.search) searchParams.set('search', params.search)
  if (params.page) searchParams.set('page', params.page.toString())
  if (params.limit) searchParams.set('limit', params.limit.toString())

  const response = await apiClient.get(`/patients?${searchParams}`)
  return response.data
}

export async function createPatient(data: CreatePatientRequest): Promise<Patient> {
  const response = await apiClient.post('/patients', data)
  return response.data
}

export async function getPatientById(id: string): Promise<Patient> {
  const response = await apiClient.get(`/patients/${id}`)
  return response.data
}

// lib/validations/patient.ts
import { z } from 'zod'

export const patientSchema = z.object({
  name: z
    .string()
    .min(2, 'Nama minimal 2 karakter')
    .max(100, 'Nama maksimal 100 karakter'),
  nik: z
    .string()
    .length(16, 'NIK harus 16 digit')
    .regex(/^\d+$/, 'NIK hanya boleh berisi angka'),
  phone: z
    .string()
    .min(10, 'Nomor telepon minimal 10 digit')
    .max(15, 'Nomor telepon maksimal 15 digit')
    .regex(/^\+?[\d\s-()]+$/, 'Format nomor telepon tidak valid'),
  address: z
    .string()
    .min(10, 'Alamat minimal 10 karakter')
    .max(500, 'Alamat maksimal 500 karakter'),
  bpjsNumber: z
    .string()
    .optional()
    .or(z.literal(''))
    .transform(val => val === '' ? undefined : val),
})

export type PatientFormData = z.infer<typeof patientSchema>

// lib/hooks/use-patients.ts
'use client'

import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query'
import { getPatients, createPatient, getPatientById } from '@/lib/api/patients'
import type { CreatePatientRequest } from '@/types/patient'

export function usePatients(params: {
  search?: string
  page?: number
  limit?: number
}) {
  return useQuery({
    queryKey: ['patients', params],
    queryFn: () => getPatients(params),
    staleTime: 5 * 60 * 1000, // 5 minutes
  })
}

export function usePatient(id: string) {
  return useQuery({
    queryKey: ['patient', id],
    queryFn: () => getPatientById(id),
    enabled: !!id,
  })
}

export function useCreatePatient() {
  const queryClient = useQueryClient()
  
  return useMutation({
    mutationFn: createPatient,
    onSuccess: () => {
      // Invalidate patients list
      queryClient.invalidateQueries({ queryKey: ['patients'] })
    },
  })
}
```

**Rules:**
- TanStack Query untuk data fetching
- Zod untuk validation schemas
- Custom hooks untuk reusable logic
- Proper TypeScript types

## Cross-Layer Communication Rules

### Data Flow Pattern
```typescript
// ✅ CORRECT: Unidirectional data flow
Page (Server Component) 
  → Feature Component (Client Component)
    → UI Component
      → Lib/API

// ❌ WRONG: Direct API calls in UI components
UI Component → API directly
```

### State Management Strategy
```typescript
// ✅ Server state dengan TanStack Query
function PatientList() {
  const { data: patients, isLoading } = usePatients({ page: 1 })
  // ...
}

// ✅ Client state dengan useState/useReducer
function PatientForm() {
  const [isSubmitting, setIsSubmitting] = useState(false)
  // ...
}

// ✅ Global client state dengan Zustand (when needed)
import { useAuthStore } from '@/store/auth'

function Navigation() {
  const { user, logout } = useAuthStore()
  // ...
}

// ❌ WRONG: Props drilling for shared state
<Component1 user={user} onUserChange={setUser} />
  <Component2 user={user} onUserChange={setUser} />
    <Component3 user={user} onUserChange={setUser} />
```

### Component Composition
```typescript
// ✅ CORRECT: Composition pattern
<Dialog>
  <DialogTrigger asChild>
    <Button>Tambah Pasien</Button>
  </DialogTrigger>
  <DialogContent>
    <DialogHeader>
      <DialogTitle>Tambah Pasien Baru</DialogTitle>
    </DialogHeader>
    <PatientForm />
  </DialogContent>
</Dialog>

// ❌ WRONG: Monolithic components
<PatientDialog 
  showAddButton={true}
  buttonText="Tambah Pasien"
  title="Tambah Pasien Baru"
  // ... many props
/>
```

## Healthcare-Specific Patterns

### Medical Form Handling
```typescript
// components/features/medical/medical-form.tsx
export function MedicalRecordForm() {
  const form = useForm<MedicalRecordData>({
    resolver: zodResolver(medicalRecordSchema),
  })

  // Auto-save draft for medical forms
  const { mutate: saveDraft } = useSaveDraft()
  
  useEffect(() => {
    const timer = setTimeout(() => {
      const formData = form.getValues()
      if (Object.keys(form.formState.dirtyFields).length > 0) {
        saveDraft(formData)
      }
    }, 30000) // Auto-save every 30 seconds

    return () => clearTimeout(timer)
  }, [form.formState.dirtyFields])

  return (
    <form onSubmit={form.handleSubmit(onSubmit)}>
      {/* Medical form fields with proper validation */}
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div className="space-y-2">
          <label htmlFor="diagnosis" className="text-sm font-medium required">
            Diagnosis Utama
          </label>
          <MedicalSelect
            id="diagnosis"
            {...form.register('primaryDiagnosis')}
            options={diagnosisOptions}
            searchable
            required
            aria-describedby="diagnosis-error"
          />
          {form.formState.errors.primaryDiagnosis && (
            <p id="diagnosis-error" className="text-sm text-red-600" role="alert">
              {form.formState.errors.primaryDiagnosis.message}
            </p>
          )}
        </div>
      </div>
      
      {/* Save and Submit buttons */}
      <div className="flex justify-end space-x-4">
        <Button type="button" variant="outline" onClick={saveDraft}>
          Simpan Draft
        </Button>
        <Button type="submit">Simpan Rekam Medis</Button>
      </div>
    </form>
  )
}
```

### Queue Management Interface
```typescript
// components/features/queue/queue-board.tsx
'use client'

export function QueueBoard() {
  const { data: queueData } = useQuery({
    queryKey: ['queue'],
    queryFn: getQueueData,
    refetchInterval: 30000, // Refresh every 30 seconds
  })

  return (
    <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <div className="lg:col-span-2">
        <div className="bg-card rounded-lg p-6">
          <h2 className="text-xl font-semibold mb-4">Antrian Saat Ini</h2>
          <div className="space-y-4">
            {queueData?.currentQueue.map((item) => (
              <QueueItem
                key={item.id}
                patient={item.patient}
                queueNumber={item.queueNumber}
                status={item.status}
                estimatedTime={item.estimatedTime}
              />
            ))}
          </div>
        </div>
      </div>
      
      <div className="space-y-6">
        <QueueStats stats={queueData?.stats} />
        <QueueControls />
      </div>
    </div>
  )
}
```

### BPJS Integration Components
```typescript
// components/features/bpjs/bpjs-verification.tsx
export function BPJSVerification({ patientId }: { patientId: string }) {
  const [isVerifying, setIsVerifying] = useState(false)
  const { mutate: verifyBPJS } = useMutation({
    mutationFn: verifyBPJSParticipant,
    onSuccess: (data) => {
      toast({
        title: 'Verifikasi Berhasil',
        description: `Status BPJS: ${data.status}`,
      })
    },
    onError: (error) => {
      toast({
        title: 'Verifikasi Gagal',
        description: error.message,
        variant: 'destructive',
      })
    },
  })

  const handleVerify = async () => {
    setIsVerifying(true)
    try {
      await verifyBPJS(patientId)
    } finally {
      setIsVerifying(false)
    }
  }

  return (
    <div className="border rounded-lg p-4">
      <div className="flex items-center justify-between">
        <h3 className="font-medium">Verifikasi BPJS</h3>
        <Button
          onClick={handleVerify}
          disabled={isVerifying}
          size="sm"
        >
          {isVerifying ? 'Memverifikasi...' : 'Verifikasi'}
        </Button>
      </div>
    </div>
  )
}
```

## Testing Strategy

### Component Testing
```typescript
// __tests__/components/patient-form.test.tsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import { PatientForm } from '@/components/features/patient/patient-form'

// Mock the API
jest.mock('@/lib/api/patients', () => ({
  createPatient: jest.fn(),
}))

describe('PatientForm', () => {
  it('renders all required fields', () => {
    render(<PatientForm />)
    
    expect(screen.getByLabelText(/nama lengkap/i)).toBeInTheDocument()
    expect(screen.getByLabelText(/nik/i)).toBeInTheDocument()
    expect(screen.getByRole('button', { name: /simpan/i })).toBeInTheDocument()
  })

  it('shows validation errors for invalid input', async () => {
    const user = userEvent.setup()
    render(<PatientForm />)
    
    const submitButton = screen.getByRole('button', { name: /simpan/i })
    await user.click(submitButton)
    
    await waitFor(() => {
      expect(screen.getByText(/nama minimal 2 karakter/i)).toBeInTheDocument()
      expect(screen.getByText(/nik harus 16 digit/i)).toBeInTheDocument()
    })
  })

  it('submits form with valid data', async () => {
    const mockCreatePatient = require('@/lib/api/patients').createPatient
    mockCreatePatient.mockResolvedValue({ id: 1 })
    
    const user = userEvent.setup()
    render(<PatientForm />)
    
    await user.type(screen.getByLabelText(/nama lengkap/i), 'John Doe')
    await user.type(screen.getByLabelText(/nik/i), '1234567890123456')
    
    const submitButton = screen.getByRole('button', { name: /simpan/i })
    await user.click(submitButton)
    
    await waitFor(() => {
      expect(mockCreatePatient).toHaveBeenCalledWith({
        name: 'John Doe',
        nik: '1234567890123456',
        // ... other fields
      })
    })
  })
})
```

### Accessibility Testing
```typescript
// __tests__/accessibility/patient-form.a11y.test.tsx
import { render } from '@testing-library/react'
import { axe, toHaveNoViolations } from 'jest-axe'
import { PatientForm } from '@/components/features/patient/patient-form'

expect.extend(toHaveNoViolations)

describe('PatientForm Accessibility', () => {
  it('should not have accessibility violations', async () => {
    const { container } = render(<PatientForm />)
    const results = await axe(container)
    expect(results).toHaveNoViolations()
  })

  it('should have proper form labels', () => {
    render(<PatientForm />)
    
    // All form inputs should have associated labels
    const nameInput = screen.getByLabelText(/nama lengkap/i)
    const nikInput = screen.getByLabelText(/nik/i)
    
    expect(nameInput).toHaveAttribute('aria-describedby')
    expect(nikInput).toHaveAttribute('aria-describedby')
  })
})
```

## Common Anti-patterns to Avoid

### 1. ❌ Server Components with Client-Only Features
```typescript
// DON'T DO THIS - Server Component with useState
export default async function PatientPage() {
  const [isOpen, setIsOpen] = useState(false) // ERROR: useState in Server Component
  
  return <div>...</div>
}
```

### 2. ❌ Direct API Calls in Components
```typescript
// DON'T DO THIS - Direct fetch in component
export function PatientList() {
  const [patients, setPatients] = useState([])
  
  useEffect(() => {
    fetch('/api/patients') // Use TanStack Query instead
      .then(res => res.json())
      .then(setPatients)
  }, [])
}
```

### 3. ❌ Prop Drilling
```typescript
// DON'T DO THIS - Passing props through many levels
<PatientPage user={user}>
  <PatientHeader user={user}>
    <UserMenu user={user} />
  </PatientHeader>
  <PatientContent user={user}>
    <PatientForm user={user} />
  </PatientContent>
</PatientPage>
```

### 4. ❌ Missing Error Boundaries
```typescript
// DON'T DO THIS - No error handling
export default function PatientPage() {
  return (
    <div>
      <PatientForm /> {/* What if this throws an error? */}
    </div>
  )
}

// DO THIS - Proper error boundary
export default function PatientPage() {
  return (
    <ErrorBoundary fallback={<ErrorFallback />}>
      <PatientForm />
    </ErrorBoundary>
  )
}
```

## Performance Optimization

### Code Splitting
```typescript
// Lazy load heavy components
const ReportGenerator = lazy(() => import('@/components/features/reports/report-generator'))

export function ReportsPage() {
  return (
    <Suspense fallback={<ReportGeneratorSkeleton />}>
      <ReportGenerator />
    </Suspense>
  )
}
```

### Image Optimization
```typescript
// Use Next.js Image component for medical images
import Image from 'next/image'

export function PatientPhoto({ src, alt }: { src: string; alt: string }) {
  return (
    <Image
      src={src}
      alt={alt}
      width={200}
      height={200}
      className="rounded-lg object-cover"
      priority={false}
      placeholder="blur"
      blurDataURL="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQ..."
    />
  )
}
```

### Bundle Analysis
```typescript
// Analyze bundle size regularly
const withBundleAnalyzer = require('@next/bundle-analyzer')({
  enabled: process.env.ANALYZE === 'true',
})

module.exports = withBundleAnalyzer({
  // Next.js config
})
```

Ikuti instruksi ini untuk memastikan frontend Next.js SIMPUS mengikuti component architecture best practices dan dapat memberikan user experience yang optimal untuk staff Puskesmas.
