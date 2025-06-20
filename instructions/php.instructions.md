---
language: php
description: "Instruksi khusus PHP untuk SIMPUS (CakePHP, CodeIgniter, PHP murni)"
---

# PHP Instructions for SIMPUS

## Naming Conventions
- Gunakan camelCase untuk variabel dan fungsi
- Gunakan PascalCase untuk class
- Konstanta dengan UPPER_SNAKE_CASE
- Prefix model dengan nama domain jika perlu (misal: PatientModel)
- File class: satu class per file, nama file = nama class

## Common Patterns
- MVC untuk CakePHP/CodeIgniter
- Gunakan prepared statement untuk query database
- Pisahkan logic validasi, akses data, dan presentasi
- Gunakan helper/utilities untuk kode reusable
- Tambahkan komentar pada blok logika kompleks

## Error Handling
- Gunakan try-catch untuk operasi eksternal (DB, file, API)
- Tampilkan pesan error yang jelas, log detail error ke file/log system
- Jangan expose stack trace ke user
- Validasi semua input sebelum proses

## Performance Considerations
- Query DB dengan index yang tepat
- Hindari N+1 query
- Cache hasil query berat jika memungkinkan
- Gunakan limit/pagination untuk data besar
- Optimasi loop dan memory usage

## Testing Patterns
- Gunakan PHPUnit untuk unit test (legacy)
- Simulasikan request untuk controller test
- Mock dependency eksternal
- Tambahkan test untuk edge case dan error handling
- Dokumentasikan skenario test di komentar

---

# Integration Guidance
- Simpan file ini di `.github/instructions/php.instructions.md`
- Gunakan instruksi ini untuk semua kode PHP, baik legacy maupun integrasi baru
- Update jika ada perubahan standar atau framework
