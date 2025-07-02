---
applyTo: "**/*.dart,**/flutter/**"
version: "1.0.0"
last_updated: "2025-07-03"
---

# Flutter Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Flutter di proyek.

## Standar Penamaan
- Ikuti konvensi Dart untuk penamaan variabel, fungsi, kelas, dan file.
- Gunakan PascalCase untuk widget dan kelas.

## Format dan Gaya
- Gunakan 2 spasi untuk indentasi.
- Ikuti pedoman dartfmt.
- Komentar pada bagian widget kompleks dan layout.

## Praktik Terbaik
- Terapkan arsitektur yang jelas (BLoC, Provider, dsb).
- Pisahkan UI, business logic, dan data layer.
- Gunakan dependency injection.
- Buat widget reusable.
- Pilih state management sesuai kebutuhan.
- Optimalkan performa dengan const, RepaintBoundary, dsb.
- Ikuti pedoman Material/Cupertino.
- Gunakan ThemeData dan MediaQuery untuk styling dan responsivitas.
- Implementasikan dark mode dan aksesibilitas.
- Gunakan named routes dan router untuk navigasi.

## Pengujian
- Tulis widget test, unit test, dan integration test.
- Mock dependency eksternal.
- Uji edge case dan error scenario.

## Contoh
// Tambahkan contoh kode Flutter sesuai standar di sini jika diperlukan.

## Referensi
- https://flutter.dev/docs/development/ui/interactive
- Dokumentasi internal proyek
