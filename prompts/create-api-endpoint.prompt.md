---
mode: "agent"
version: "1.0.0"
last_updated: "2025-07-03"
description: "Membuat endpoint API baru sesuai standar RESTful dan praktik terbaik keamanan."
---
# Create a New API Endpoint

Buat endpoint API baru dengan karakteristik berikut:

1. **Definisi Endpoint**:
   - HTTP method (GET, POST, PUT, DELETE, dll)
   - Path dan parameter path
   - Query parameter (jika ada)
   - Skema request body (jika ada)

2. **Validasi Input**:
   - Validasi semua parameter
   - Tangani input tidak valid dengan baik

3. **Autentikasi & Otorisasi**:
   - Terapkan middleware autentikasi
   - Implementasi pengecekan otorisasi

4. **Logika Bisnis**:
   - Implementasi fungsionalitas utama
   - Query database atau API eksternal
   - Tangani edge case dan error

5. **Respons**:
   - Status code yang sesuai
   - Struktur response body sesuai konvensi API
   - Pesan error yang jelas

6. **Dokumentasi**:
   - Komentar dokumentasi API
   - Format request/response
   - Contoh penggunaan

7. **Pengujian**:
   - Unit test untuk endpoint
   - Integration test jika perlu

Ikuti prinsip RESTful dan struktur API proyek. Pastikan penanganan error dan keamanan sudah baik.
