---
applyTo: "**/*.py"
version: "1.0.0"
last_updated: "2025-07-03"
---
# Python Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Python di proyek.

## Standar Penamaan
- snake_case untuk variabel dan fungsi
- PascalCase untuk kelas
- UPPER_CASE untuk konstanta
- Prefix _ untuk anggota privat

## Format dan Gaya
- Ikuti PEP 8
- 4 spasi untuk indentasi
- Panjang baris < 88 karakter (standar Black)
- Gunakan double quotes untuk string

## Praktik Terbaik
- Gunakan type hint
- Docstring untuk fungsi, kelas, modul
- Context manager (with) untuk resource
- "Explicit is better than implicit"
- List/dict/set comprehension
- Prefer built-in/standard library

## Penanganan Kesalahan
- Exception spesifik
- Hanya catch exception yang bisa ditangani
- finally untuk cleanup
- Prefer context manager

## Pengujian
- pytest untuk unit test
- Fungsi test kecil dan fokus
- Nama fungsi test deskriptif
- Fixture untuk setup data
- Parametrize test serupa

## Contoh
Tambahkan contoh kode Python sesuai standar di sini jika diperlukan.

## Referensi
- https://peps.python.org/pep-0008/
- https://docs.python.org/3/tutorial/
