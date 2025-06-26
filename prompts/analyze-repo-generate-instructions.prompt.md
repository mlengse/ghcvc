---
mode: "agent"
description: "Analyze repository and generate custom instructions"
---
# Repository Analysis and Instructions Generation

## Repository Analysis

Analyze the current repository structure and codebase to understand:

1. **Architecture**: The overall architectural pattern(s) used in the project (e.g., MVC, MVVM, Clean Architecture, Microservices)
2. **Technologies**: Primary programming languages, frameworks, libraries, and tools used in the project
3. **Organization**: The directory structure, module organization, and code separation principles
4. **Conventions**: Coding standards, naming conventions, and style patterns present in the codebase
5. **Domain**: The business domain and key concepts represented in the codebase

## Custom Instructions Generation

Berdasarkan analisis di atas, buat file instructions dengan format dan penamaan berikut:

- Simpan file sebagai `instructions/<nama-bahasa/tujuan>.instructions.md`.
- Gunakan metadata front matter berikut di bagian atas file:
  ```yaml
  ---
  applyTo: "**/*.ext" # sesuaikan glob pattern file yang relevan
  version: "1.0.0"
  last_updated: "YYYY-MM-DD"
  ---
  ```

Isi file instructions harus mencakup:

1. **Project Overview**: A brief description of the project's purpose and domain
2. **Architecture Guidelines**: Instructions on how generated code should fit into the existing architecture
3. **Technology Stack**: Details on the preferred technologies and how they should be used
4. **Coding Standards**: Specific coding conventions to follow, based on observed patterns
5. **Testing Requirements**: Guidelines on how tests should be written for this project
6. **Documentation Standards**: Requirements for code comments and documentation
7. **Language-Specific Instructions**: For each primary programming language detected, include:
   - **Naming Conventions**: Specific to this project's implementation of the language
   - **Common Patterns**: Recurring code patterns observed in the codebase
   - **Error Handling**: Project-specific error handling strategies
   - **Performance Considerations**: Language-specific optimizations used in the project
   - **Testing Patterns**: How tests are typically written for this language in the project
8. **Integration Guidance**: Provide guidance on how the generated instructions relate to the repository structure and how they should be used with GitHub Copilot.

Berikan instruksi tentang:

- Di mana menyimpan file instructions di struktur repository (`instructions/`)
- Cara menggunakan instructions di dalam VS Code
- Cara membagikan instructions ke anggota tim
- Cara mengembangkan instructions sesuai kebutuhan proyek
