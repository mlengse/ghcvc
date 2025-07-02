---
applyTo: "**/*.php"
version: "1.0.0"
last_updated: "2025-07-03"
---

# PHP Instructions for SIMPUS

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode PHP di proyek SIMPUS, baik legacy maupun integrasi baru (CakePHP, CodeIgniter, PHP murni).

## Standar Penamaan
- Gunakan camelCase untuk variabel dan fungsi
- Gunakan PascalCase untuk class
- Konstanta dengan UPPER_SNAKE_CASE
- Prefix model dengan nama domain jika perlu (misal: PatientModel)
- File class: satu class per file, nama file = nama class

## Format dan Gaya
- Komentar pada blok logika kompleks
- Satu class per file
- Struktur MVC untuk framework

## Praktik Terbaik
- Gunakan MVC untuk CakePHP/CodeIgniter
- Gunakan prepared statement untuk query database
- Pisahkan logic validasi, akses data, dan presentasi
- Gunakan helper/utilities untuk kode reusable
- Validasi semua input sebelum proses
- Jangan expose stack trace ke user

## Pengujian
- Gunakan PHPUnit untuk unit test (legacy)
- Simulasikan request untuk controller test
- Mock dependency eksternal
- Tambahkan test untuk edge case dan error handling
- Dokumentasikan skenario test di komentar

## Contoh
// Tambahkan contoh kode PHP sesuai standar di sini jika diperlukan.

## Referensi
- Dokumentasi framework (CakePHP, CodeIgniter)
- Standar internal SIMPUS
