---
applyTo: "*"
version: "1.0.0"
last_updated: "2025-07-03"
---
# GHCVC Copilot Instructions

## Project Overview
Konfigurasi ini digunakan untuk mengatur standar, praktik terbaik, dan integrasi GitHub Copilot di seluruh proyek. Tujuannya adalah memastikan Copilot menghasilkan kode yang konsisten, aman, dan sesuai kebutuhan tim.

> **Catatan:** Proyek ini sering mengembangkan aplikasi Progressive Web App (PWA) berbasis Next.js, serta mendukung integrasi WebAssembly (WASM) menggunakan Rust.

## Architecture Guidelines
- Tidak ada framework aplikasi utama, repo ini adalah repo konfigurasi Copilot.
- Struktur modular: instruksi, mode chat, dan prompt dipisahkan per folder.
- Instruksi per bahasa/framework disimpan di `instructions/`.
- Untuk aplikasi PWA Next.js:
  - Gunakan struktur App Router dan praktik modular Next.js.
  - Implementasikan service worker, manifest, dan caching sesuai standar PWA.
- Untuk integrasi WASM/Rust:
  - Strukturkan kode Rust di folder terpisah (misal: `wasm/` atau `rust/`).
  - Gunakan toolchain seperti wasm-pack untuk build dan integrasi ke Next.js.

## Technology Stack
- Markdown untuk seluruh file konfigurasi.
- Bahasa utama: JavaScript/TypeScript, Python, Go, Dart, Flutter, React, Next.js, Rust, Kotlin, PHP.
- Next.js untuk aplikasi web modern (termasuk PWA).
- Rust untuk modul performa tinggi via WebAssembly (WASM).
- Tools: Copilot, VS Code, pengujian dengan Jest, Pytest, JUnit, PHPUnit, wasm-pack, dsb.

## Coding Standards
- Setiap file instruksi memiliki metadata front matter.
- Penamaan file: `<bahasa/tujuan>.instructions.md`.
- Heading wajib: Ruang Lingkup, Standar Penamaan, Format dan Gaya, Praktik Terbaik, Pengujian, Contoh, Referensi.
- Ikuti standar dan praktik terbaik masing-masing bahasa (lihat file di folder `instructions/`).
- Untuk PWA Next.js:
  - Ikuti best practice PWA (manifest, service worker, caching, offline support, installability, dsb).
- Untuk WASM/Rust:
  - Pastikan boundary antara JS/WASM jelas dan aman.
  - Dokumentasikan interface antara Next.js dan Rust.

## Testing Requirements
- Gunakan framework pengujian sesuai bahasa (Jest, Pytest, JUnit, PHPUnit, dsb).
- Tulis unit test, integration test, dan edge case.
- Mock dependency eksternal jika perlu.
- Untuk PWA:
  - Uji offline mode, caching, dan installability.
- Untuk WASM:
  - Uji boundary dan interoperabilitas JS <-> WASM.

## Documentation Standards
- Sertakan docstring/komentar pada fungsi, kelas, dan modul publik.
- Dokumentasikan parameter, return value, dan contoh penggunaan.
- Update dokumentasi setiap ada perubahan kode.
- Untuk integrasi Next.js + WASM, tambahkan diagram atau penjelasan alur data jika perlu.

## Language-Specific Instructions
- Lihat file instruksi per bahasa di folder `instructions/` untuk detail:
  - **JavaScript/TypeScript**: `javascript.instructions.md`
  - **Python**: `python.instructions.md`
  - **Go**: `go.instructions.md`
  - **Dart**: `dart.instructions.md`
  - **Flutter**: `flutter.instructions.md`
  - **React**: `react.instructions.md`
  - **Next.js**: `nextjs.instructions.md` (termasuk guideline PWA)
  - **Rust**: `rust.instructions.md` (termasuk guideline WASM)
  - **Kotlin**: `kotlin.instructions.md`
  - **PHP**: `php.instructions.md`

## Integration Guidance
- Simpan file instruksi di folder `instructions/`.
- Pastikan folder `instructions/` sudah terdaftar di `settings.json` pada key `chat.instructionsFilesLocations`.
- Untuk menambah folder lain, tambahkan ke array di `settings.json`:
  ```json
  "chat.instructionsFilesLocations": [
    "./instructions",
    "./.github/instructions",
    "./folder-lain"
  ]
  ```
- Untuk menggunakan instruksi di VS Code:
  - Pastikan Copilot Chat sudah aktif.
  - Instruksi akan diterapkan otomatis sesuai file yang diedit.
- Untuk membagikan instruksi ke tim:
  - Commit dan push file instruksi ke repository.
  - Informasikan ke anggota tim untuk pull perubahan.
- Untuk mengembangkan instruksi:
  - Tambahkan atau update file di folder `instructions/`.
  - Ikuti format dan struktur yang sudah ada.
  - Update metadata dan dokumentasi jika ada perubahan signifikan.
- Untuk aplikasi PWA Next.js dan integrasi WASM/Rust:
  - Dokumentasikan setup dan guideline khusus di file instruksi terkait.
  - Pastikan semua anggota tim memahami boundary dan best practice integrasi.
