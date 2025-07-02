---
applyTo: "**/*.js,**/*.jsx,**/*.ts,**/*.tsx,**/app/**,**/pages/**,**/public/**,**/service-worker.js,**/manifest.json"
version: "1.0.0"
last_updated: "2025-07-03"
---
# Progressive Web App (PWA) Architecture Instructions

## Architecture Overview
Arsitektur PWA di proyek ini berbasis Next.js (App Router), mengadopsi pola modular dan separation of concerns. PWA menggabungkan keunggulan web dan aplikasi native: offline support, installability, push notification, dan caching cerdas.

- Struktur utama: `app/`, `pages/`, `public/`, `service-worker.js`, `manifest.json`.
- Service worker mengelola caching, offline, dan background sync.
- Manifest mendefinisikan metadata aplikasi (ikon, warna, dsb).

## Layer-Specific Guidelines
- **Presentation Layer**: Komponen UI (React/Next.js), styling, dan interaksi user.
- **Service Worker Layer**: File `service-worker.js` untuk caching, offline, dan push notification.
- **Manifest Layer**: File `manifest.json` untuk metadata aplikasi.
- **Data Layer**: API call, state management (Context, Redux, dsb), dan storage (IndexedDB, localStorage).

## Cross-Layer Communication
- Komunikasi antara UI dan service worker via postMessage/event.
- Service worker intercept fetch event untuk caching dan offline.
- Update UI berdasarkan status koneksi (online/offline) dan notifikasi dari service worker.
- Sinkronisasi data saat kembali online (background sync).

## Testing Approach
- Unit test untuk komponen UI (React Testing Library, Jest).
- Integration test untuk flow utama (Cypress, Playwright).
- Test service worker: caching, offline, push notification, update.
- Test manifest: validasi manifest, installability, dan icon.
- Uji edge case: offline mode, update service worker, fallback.

## Common Anti-patterns
- Tidak memisahkan logic service worker dan UI.
- Tidak menghandle update service worker dengan benar (stale cache).
- Tidak menguji offline mode dan fallback.
- Meng-cache semua request tanpa strategi (cache bloat).
- Tidak mengupdate manifest saat branding berubah.

## Implementation Guidance
- Simpan file PWA utama di `public/` (`manifest.json`, `service-worker.js`).
- Gunakan Next.js App Router untuk modularitas dan SSR/SSG.
- Implementasikan strategi caching (cache-first, network-first, dsb) sesuai kebutuhan.
- Dokumentasikan flow update service worker dan fallback.
- Tambahkan contoh penggunaan PWA di README atau dokumentasi proyek.
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
