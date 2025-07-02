---
mode: "agent"
description: "Design custom chat mode for specific project role"
---
# Custom Chat Mode Generator

## Repository Context Analysis

First, analyze the current repository to understand:

1. **Project Domain**: The business or technical domain of the project
2. **Key User Roles**: The main roles involved in development (e.g., frontend developer, API developer, database administrator)
3. **Common Tasks**: Recurring tasks performed by each role
4. **Technology Stack**: The primary technologies used in each area of the project

## Chat Mode Definition

Berdasarkan analisis di atas, buat file chatmode dengan format dan penamaan berikut:

- Simpan file sebagai `chatmodes/<nama-mode>.chatmode.md`.
- Gunakan metadata front matter berikut di bagian atas file:
  ```yaml
  ---
  description: "Deskripsi singkat tentang tujuan mode chat ini"
  tools: ["codebase", "selection", ...] # sesuaikan tools yang dibutuhkan
  ---
  ```

Isi file chatmode harus mencakup:

1. **Main Instructions**:
   - Penjelasan tujuan dan fokus mode chat
   - Panduan spesifik untuk peran/role
   - Pengetahuan domain dan pola umum
   - Batasan dan tanggung jawab

2. **Task-Specific Guidelines**:
   - Instruksi untuk tugas umum
   - Pendekatan pemecahan masalah
   - Integrasi dengan peran/sistem lain
   - Standar kualitas khusus

3. **Communication Style**:
   - Struktur respons
   - Tingkat detail teknis
   - Terminologi dan gaya bahasa

## VS Code Integration

Jika folder custom chatmode (`chatmodes/`, `.github/chatmodes/`, atau lainnya) belum terdaftar di settings.json, tambahkan entri berikut pada settings.json workspace:
```json
"chat.modeFilesLocations": [
  "./chatmodes",
  "./.github/chatmodes",
  "./folder-lain"
]
```
Pastikan perubahan tersimpan agar Copilot mengenali file chatmode di folder tersebut.

Berikan instruksi tentang:
- Di mana menyimpan file chatmode di struktur repository (`chatmodes/`)
- Cara menggunakan chatmode di dalam VS Code
- Cara membagikan chatmode ke anggota tim
- Cara mengembangkan chatmode sesuai kebutuhan proyek
