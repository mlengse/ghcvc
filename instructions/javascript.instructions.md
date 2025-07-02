---
applyTo: "**/*.js,**/*.jsx,**/*.ts,**/*.tsx"
version: "1.0.0"
last_updated: "2025-07-03"
---

# JavaScript and TypeScript Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode JavaScript dan TypeScript di proyek.

## Standar Penamaan
- camelCase untuk variabel dan fungsi
- PascalCase untuk class dan komponen React
- UPPER_CASE untuk konstanta
- Prefix private class field dengan _

## Format dan Gaya
- 2 spasi untuk indentasi
- Semicolon di akhir statement
- Panjang baris < 100 karakter
- Single quote untuk string

## Praktik Terbaik
- Gunakan async/await
- Gunakan const untuk variabel tetap
- Prefer destructuring
- Gunakan spread operator
- Gunakan optional chaining dan nullish coalescing
- Prefer map/filter/reduce

## Pengujian
- Gunakan Jest untuk testing
- Test komponen dengan React Testing Library
- Mock dependency eksternal
- Fokus pada testing behavior

## Contoh
// Tambahkan contoh kode JS/TS sesuai standar di sini jika diperlukan.

## Referensi
- https://github.com/airbnb/javascript
- Dokumentasi internal proyek
