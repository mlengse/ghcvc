---
mode: "agent"
description: "Generate architecture-specific instructions"
---
# Architecture-Specific Instructions Generator

## Architecture Analysis

First, analyze the architectural patterns present in the repository:

1. **Architectural Pattern**: Identify the primary architectural pattern(s) in use (e.g., Clean Architecture, MVVM, Hexagonal, Microservices)
2. **Layer Separation**: How are concerns separated (e.g., presentation, business logic, data access)
3. **Component Communication**: How do components interact within and across layers
4. **Dependency Management**: How dependencies are managed and injected
5. **Cross-Cutting Concerns**: How aspects like logging, error handling, and security are addressed

## Custom Instructions Creation

Berdasarkan analisis di atas, buat file instructions dengan format dan penamaan berikut:

- Simpan file sebagai `instructions/<nama-arsitektur>.instructions.md`.
- Gunakan metadata front matter berikut di bagian atas file:
  ```yaml
  ---
  applyTo: "**/*.ext" # sesuaikan glob pattern file yang relevan
  version: "1.0.0"
  last_updated: "YYYY-MM-DD"
  ---
  ```

Isi file instructions harus mencakup:

1. **Architecture Overview**
2. **Layer-Specific Guidelines**
3. **Cross-Layer Communication**
4. **Testing Approach**
5. **Common Anti-patterns**
6. **Implementation Guidance**

Berikan instruksi tentang:
- Di mana menyimpan file instructions di struktur repository (`instructions/`)
- Cara menggunakan instructions di dalam VS Code
- Cara membagikan instructions ke anggota tim
- Cara mengembangkan instructions sesuai kebutuhan proyek
