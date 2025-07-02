---
mode: "agent"
description: "Design custom prompt template for recurring project task"
---
# Custom Prompt Template Generator

## Task Analysis

First, analyze the specific recurring task in the repository that requires a custom prompt:

1. **Task Purpose**: What is the goal of this task in the project context?
2. **Task Frequency**: How often is this task performed?
3. **Typical Steps**: What are the standard steps to complete this task?
4. **Required Context**: What context is needed to perform this task effectively?
5. **Common Challenges**: What difficulties or edge cases typically arise?
6. **Related Components**: Which parts of the codebase are typically involved?

## Prompt Template Creation

Based on this analysis, generate a custom prompt template file dengan format dan penamaan berikut:

- Simpan file sebagai `prompts/<nama-tugas>.prompt.md`.
- Gunakan metadata front matter berikut di bagian atas file:
  ```yaml
  ---
  mode: "agent" # atau "ask"/"edit" sesuai kebutuhan
  description: "Deskripsi singkat tentang tujuan prompt ini"
  ---
  ```

Isi file prompt harus mencakup:

1. **Main Prompt Content**:
   - Clear title describing the task
   - Structured sections that guide completion of the task
   - Placeholders for task-specific inputs
   - Required context references (#file, #selection, etc.)
   - Guidance on expected output format

2. **Task-Specific Guidelines**:
   - Project-specific requirements for this task
   - Quality standards to meet
   - Common pitfalls to avoid
   - Integration points to consider

3. **Documentation**:
   - Usage examples
   - When to use this prompt vs. alternatives
   - How to customize for specific instances of the task

## VS Code Integration

Jika folder custom prompt (`prompts/` atau lainnya) belum terdaftar di settings.json, tambahkan entri berikut pada settings.json workspace:
```json
"chat.promptFilesLocations": [
  "./prompts",
  "./folder-lain"
]
```
Pastikan perubahan tersimpan agar Copilot mengenali file prompt di folder tersebut.

Berikan instruksi tentang:
- Di mana menyimpan file prompt di struktur repository (`prompts/`)
- Cara menggunakan prompt di dalam VS Code
- Cara membagikan prompt ke anggota tim
- Cara mengembangkan prompt sesuai perubahan kebutuhan proyek
