---
applyTo: "**/*.rs,**/*.wasm,**/wasm*/**"
version: "1.0.0"
last_updated: "2025-07-03"
---
# WebAssembly (WASM) Architecture Instructions

## Architecture Overview
Arsitektur WASM di proyek ini digunakan untuk mengintegrasikan modul performa tinggi (biasanya ditulis dengan Rust) ke dalam aplikasi web (misal: Next.js). WASM memungkinkan eksekusi kode native di browser dengan performa mendekati native, serta interoperabilitas dengan JavaScript.

- Modul Rust/WASM ditempatkan di folder khusus (misal: `wasm/` atau `rust/`).
- Build menggunakan toolchain seperti wasm-pack.
- Integrasi dengan aplikasi web dilakukan melalui interface JavaScript (bindings).

## Layer-Specific Guidelines
- **WASM Layer**: Berisi kode Rust yang dikompilasi ke WebAssembly. Fokus pada logika performa tinggi, komputasi berat, atau kebutuhan low-level.
- **JS/TS Integration Layer**: Berisi kode JavaScript/TypeScript yang memanggil modul WASM. Bertanggung jawab untuk serialisasi data, error handling, dan bridging antara dunia JS dan WASM.
- **App Layer**: Aplikasi Next.js/React yang menggunakan API dari WASM melalui JS bindings.

## Cross-Layer Communication
- Gunakan interface yang jelas dan terdokumentasi antara Rust dan JS (misal: via wasm-bindgen).
- Hindari passing data besar secara langsung, gunakan buffer atau shared memory jika perlu.
- Tangani error di boundary JS <-> WASM secara eksplisit, konversi error Rust ke JS Error.
- Dokumentasikan tipe data dan kontrak API antara layer.

## Testing Approach
- Unit test untuk kode Rust sebelum dikompilasi ke WASM (gunakan cargo test).
- Integration test untuk boundary JS <-> WASM (gunakan test runner JS/TS, misal Jest).
- Uji interoperabilitas dan edge case (misal: data invalid, error handling, performance regression).
- Gunakan test automation untuk build dan test pipeline.

## Common Anti-patterns
- Menulis seluruh aplikasi di WASM (gunakan hanya untuk bagian performa kritis).
- Tidak membatasi boundary antara JS dan WASM (harus jelas dan minimal).
- Tidak mengelola memory/heap dengan benar (hindari memory leak di Rust/WASM).
- Tidak mengkonversi error dengan baik antara Rust dan JS.
- Tidak mendokumentasikan interface dan kontrak data.

## Implementation Guidance
- Simpan seluruh kode WASM di folder khusus (`wasm/` atau `rust/`).
- Gunakan wasm-pack untuk build dan generate bindings.
- Dokumentasikan setiap fungsi publik yang diekspos ke JS.
- Pastikan boundary dan kontrak API terdokumentasi di README atau docstring.
- Tambahkan contoh penggunaan di Next.js/React.
- Update instruksi jika ada perubahan arsitektur atau toolchain.

## VS Code Integration
- Simpan file instruksi ini di folder `instructions/`.
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
