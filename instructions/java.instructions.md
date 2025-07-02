---
applyTo: "**/*.java"
version: "1.0.0"
last_updated: "2025-07-03"
---

# Java Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Java di proyek.

## Standar Penamaan
- camelCase untuk variabel dan method
- PascalCase untuk class dan interface
- UPPER_SNAKE_CASE untuk konstanta
- Nama package huruf kecil semua

## Format dan Gaya
- 4 spasi untuk indentasi
- Panjang baris < 120 karakter
- Gunakan braces untuk semua blok
- Braces di baris yang sama
- Spasi setelah keyword (if, for, while)

## Praktik Terbaik
- Favor composition over inheritance
- Field private, gunakan getter/setter
- Gunakan interface untuk kontrak
- Minimalkan visibility method
- Prefer immutable object
- Gunakan stream/functional programming jika sesuai

## Pengujian
- Gunakan JUnit untuk unit test
- Mock dependency dengan Mockito
- Uji edge case dan error
- Ikuti pola AAA (Arrange, Act, Assert)

## Contoh
// Tambahkan contoh kode Java sesuai standar di sini jika diperlukan.

## Referensi
- https://www.oracle.com/java/technologies/javase/codeconventions-150003.pdf
- Dokumentasi internal proyek
