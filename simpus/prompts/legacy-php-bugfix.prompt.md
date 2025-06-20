---
mode: "ask"
description: "Prompt template untuk patch keamanan dan bugfix pada sistem legacy PHP SIMPUS. Memastikan perubahan aman, terdokumentasi, dan teruji."
---

# Legacy PHP Security Patch & Bugfix Prompt

## Tujuan
Bantu developer melakukan patch keamanan atau bugfix pada sistem legacy PHP (j-care, antrian, bpjsantrian, siappkm_bpjs) dengan standar keamanan dan dokumentasi SIMPUS.

## Instruksi Penggunaan
1. Jelaskan bug/celah keamanan yang ditemukan.
2. Sertakan file dan lokasi kode yang terlibat (#file, #selection).
3. Jelaskan langkah perbaikan yang diusulkan.
4. Tulis snippet kode sebelum & sesudah perubahan (jika perlu).
5. Sertakan langkah testing dan hasilnya.
6. Tambahkan catatan rollback jika perubahan berisiko.
7. Update changelog dan dokumentasi terkait.

---

## Template Prompt

### [Deskripsi Masalah]
- Jenis: [Bug/Security Patch]
- Sistem: [j-care/antrian/bpjsantrian/siappkm_bpjs]
- Lokasi: [#file, #selection]
- Ringkasan masalah: [Jelaskan bug/celah keamanan]

### [Solusi yang Diusulkan]
- Langkah perbaikan: [Jelaskan langkah teknis]
- Snippet kode sebelum: [kode lama]
- Snippet kode sesudah: [kode baru]
- Validasi input/sanitasi: [Ya/Tidak, jelaskan]
- Query database: [Gunakan prepared statement jika perlu]

### [Testing & Dokumentasi]
- Langkah testing: [Manual/unit test]
- Hasil testing: [Lulus/gagal, detail]
- Catatan rollback: [Langkah rollback jika perlu]
- Changelog: [Update changelog terkait]

---

## Standar & Tips
- Prioritaskan keamanan (SQLi, XSS, CSRF, session, upload)
- Jangan simpan credential di kode
- Tambahkan komentar pada kode yang diubah
- Jaga kompatibilitas mundur

---

## Contoh Penggunaan

### [Deskripsi Masalah]
- Jenis: Security Patch
- Sistem: antrian
- Lokasi: antrian/koneksi.php, baris 42
- Ringkasan masalah: Query login rentan SQL injection

### [Solusi yang Diusulkan]
- Langkah perbaikan: Ganti query dengan prepared statement
- Snippet kode sebelum:
```php
$sql = "SELECT * FROM users WHERE username='$user' AND password='$pass'";
```
- Snippet kode sesudah:
```php
$stmt = $db->prepare("SELECT * FROM users WHERE username=? AND password=?");
$stmt->bind_param("ss", $user, $pass);
$stmt->execute();
```
- Validasi input/sanitasi: Ya, tambahkan filter_var pada $user
- Query database: Menggunakan prepared statement

### [Testing & Dokumentasi]
- Langkah testing: Uji login dengan input normal dan SQL injection
- Hasil testing: Lulus, SQL injection tidak berhasil
- Catatan rollback: Kembalikan ke query lama jika error
- Changelog: Tambahkan entry di CHANGELOG_LEGACY.md

---

## Integrasi & Evolusi
- Simpan file ini di `.github/prompts/legacy-php-bugfix.prompt.md`
- Gunakan prompt ini saat melakukan patch di folder legacy
- Bagikan ke tim melalui dokumentasi internal
- Update template jika ada standar baru atau kebutuhan khusus
