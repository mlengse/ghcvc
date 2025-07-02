---
applyTo: "**/*.jsx,**/*.tsx,**/*next*/**"
version: "1.0.0"
last_updated: "2025-07-03"
---
# Next.js Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Next.js di proyek.

## Standar Penamaan
- Ikuti konvensi React untuk penamaan komponen, file, dan direktori
- Gunakan PascalCase untuk komponen, camelCase untuk instance
- Gunakan nama deskriptif dan konsisten

## Format dan Gaya
- Struktur direktori standar Next.js (pages, public, styles, app)
- 4 spasi untuk indentasi
- Panjang baris maksimal 100 karakter
- Gunakan Prettier/ESLint untuk format otomatis
- Kurung kurawal di baris yang sama
- Spasi di sekitar operator

## Praktik Terbaik
- Gunakan App Router untuk proyek baru
- Komponen reusable di folder components
- Helper di lib/utils
- API route di api/
- Metadata SEO dengan Next.js metadata API
- Gunakan Link untuk navigasi
- Prefetching untuk navigasi cepat
- Gunakan Image untuk optimasi gambar
- Dynamic import untuk code splitting
- State management sesuai kebutuhan (Context, Redux, dsb)
- Validasi input di API route
- Error handling dan status code konsisten
- Gunakan NextAuth.js untuk autentikasi
- Variabel lingkungan untuk konfigurasi
- Deployment di Vercel atau platform serupa
- CI/CD pipeline

## Pengujian
- Unit test untuk komponen dan utilitas
- Integration test untuk user flow
- E2E test dengan Cypress/Playwright
- Mock API di test
- Test SSR/SSG/CSR

## Contoh
Tambahkan contoh kode Next.js sesuai standar di sini jika diperlukan.

## Referensi
- https://nextjs.org/docs
- https://nextjs.org/learn
