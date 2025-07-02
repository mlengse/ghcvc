---
applyTo: "**/*.kt,**/*.kts"
version: "1.0.0"
last_updated: "2025-07-03"
---
# Kotlin Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Kotlin di proyek.

## Standar Penamaan
- camelCase untuk variabel, fungsi, dan properti
- PascalCase untuk kelas, interface, dan objek
- SCREAMING_SNAKE_CASE untuk konstanta
- Gunakan backticks untuk identifier khusus
- Hindari prefix 'I' pada interface
- Nama deskriptif dan bermakna

## Format dan Gaya
- 4 spasi untuk indentasi
- Panjang baris 100-120 karakter
- Gunakan ktlint/detekt untuk format otomatis
- Kurung kurawal di baris yang sama
- Spasi di sekitar operator
- Trailing comma pada parameter multi-baris
- Format konsisten untuk fungsi/kelas multi-baris

## Praktik Terbaik
- Prefer val daripada var
- Gunakan extension function
- Data class untuk model
- Sealed class untuk hierarki terbatas
- Object declaration untuk singleton
- Companion object untuk static/factory
- Type alias untuk tipe kompleks
- Lambda dan higher-order function
- Null safety dengan anotasi
- Smart cast
- Property delegation

### Koleksi
- Factory function (listOf, mapOf, setOf)
- Scope function (let, run, with, apply, also)
- Transformasi koleksi (map, filter, reduce)
- Sequence untuk koleksi besar
- Inline function dengan reified generics

### Coroutine
- Fungsi suspend untuk async
- Scope coroutine sesuai lifecycle
- Structured concurrency
- Exception handling di coroutine
- Dispatcher sesuai kebutuhan
- Flow untuk stream reaktif

### Android (jika relevan)
- ViewModel untuk data UI
- LiveData/Flow untuk data observable
- Scope coroutine (viewModelScope, lifecycleScope)
- View binding/data binding
- Dependency injection (Hilt/Koin)
- Repository pattern

## Pengujian
- JUnit untuk unit test
- MockK untuk mocking
- TestDispatcher untuk coroutine
- runTest untuk suspend function
- InstantTaskExecutorRule untuk ViewModel
- Instrumentation test untuk komponen Android

## Contoh
Tambahkan contoh kode Kotlin sesuai standar di sini jika diperlukan.

## Referensi
- https://kotlinlang.org/docs/coding-conventions.html
- https://android.github.io/kotlin-guides/
