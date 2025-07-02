---
mode: "agent"
version: "1.0.0"
last_updated: "2025-07-03"
description: "Melakukan security review kode secara komprehensif dan memberikan rekomendasi mitigasi."
---
# Security Code Review

Lakukan security review menyeluruh pada kode berikut. Periksa:

1. **Validasi Input**:
   - Missing or insufficient validation
   - Potential injection vulnerabilities (SQL, XSS, command injection)
   - Type confusion or unsafe type casting

2. **Autentikasi & Otorisasi**:
   - Improper access controls
   - Missing authentication checks
   - Insecure credential management

3. **Keamanan Data**:
   - Sensitive data exposure
   - Improper encryption
   - Hard-coded credentials or secrets
   - Insecure data storage

4. **Manajemen Resource**:
   - Memory leaks
   - Resource exhaustion possibilities
   - Unmanaged resources

5. **Penanganan Error**:
   - Information exposure through error messages
   - Improper error handling

6. **Praktik Secure Coding**:
   - Race conditions
   - Time-of-check to time-of-use bugs
   - Insecure randomness

Untuk setiap isu:
- Deskripsi kerentanan
- Dampak potensial
- Lokasi di kode
- Rekomendasi perbaikan
