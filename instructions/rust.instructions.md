---
applyTo: "**/*.rs"
version: "1.0.0"
last_updated: "2025-07-03"
---
# Rust Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Rust di proyek.

## Standar Penamaan
- snake_case untuk variabel, fungsi, dan modul
- PascalCase untuk tipe, trait, enum variant
- SCREAMING_SNAKE_CASE untuk statik dan konstanta
- Nama deskriptif dan jelas
- Nama singkat namun bermakna

## Format dan Gaya
- rustfmt untuk format otomatis
- 4 spasi untuk indentasi
- Panjang baris 100 karakter
- Kurung buka di baris yang sama
- Spasi di sekitar operator

## Praktik Terbaik
- Result<T, E> untuk operasi yang bisa gagal
- Option<T> untuk nilai opsional
- Hindari unwrap()/expect() di production
- Error type dengan std::error::Error
- Operator ? untuk propagasi error
- thiserror/anyhow untuk error management
- Tambahkan context pada error
- Prefer borrowing daripada ownership
- Gunakan &str jika hanya baca
- Referensi dengan lifetime sesuai
- Hindari clone tidak perlu
- Cow<'a, T> untuk fleksibilitas borrow/own
- Lifetime eksplisit jika perlu
- Hindari unsafe kecuali perlu
- Dokumentasi pada blok unsafe
- Abstraksi aman untuk unsafe
- Checked arithmetic untuk overflow
- NonZeroU32 jika relevan
- Validasi input eksternal
- Modul untuk organisasi kode
- API publik minimal dan terdokumentasi
- Detail implementasi privat
- Test di modul #[cfg(test)]
- Feature flag untuk opsionalitas
- Message passing dengan channel
- Mutex/sync primitive jika perlu
- Hindari data race
- rayon untuk paralelisme
- Implementasi Send/Sync sesuai
- Dokumentasi thread safety
- Type system untuk cegah bug
- Enum untuk state/variant
- Trait untuk kontrak tipe
- Generik untuk reuse
- Associated type untuk generik kompleks
- Type-level programming jika perlu
- Dokumentasi public API dengan rustdoc
- Contoh di dokumentasi
- Dokumentasi kondisi panic
- Markdown di doc comment
- Doctest untuk validasi

## Pengujian
- Unit test untuk fungsi/metode
- #[test] untuk test
- assert!/assert_eq!/assert_ne! untuk asersi
- Integration test di folder tests/
- Property-based test jika perlu
- Benchmark untuk kode performa

## Contoh
Tambahkan contoh kode Rust sesuai standar di sini jika diperlukan.

## Referensi
- https://doc.rust-lang.org/1.0.0/style/
- https://doc.rust-lang.org/book/
