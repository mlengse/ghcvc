---
applyTo: "**/*.dart"
version: "1.0.0"
last_updated: "2025-07-03"
---

# Dart Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Dart di proyek.

## Standar Penamaan
- Use lowerCamelCase for variables, functions, and methods
- Use UpperCamelCase for classes, enum types, typedefs, and extensions
- Use lowercase_with_underscores for libraries, packages, directories, and files
- Prefix private identifiers with underscore (_)
- Use SCREAMING_CAPS for constants

## Format dan Gaya
- Use 2 spaces for indentation
- Limit lines to 80 characters when possible
- Use dartfmt (dart format) for consistent formatting
- Place the opening curly brace on the same line
- Add spaces between control flow keywords and parentheses
- Always use curly braces for control flow statements, even for single-line bodies

## Praktik Terbaik
- Prefer final for variables that don't change
- Use const for compile-time constants
- Make fields private unless they need to be accessed from outside
- Use getters/setters instead of public fields when behavior might change
- Avoid using dynamic unless necessary
- Use collection literals instead of constructors
- Use cascades (..) to chain operations on the same object
- Use async/await for asynchronous code instead of raw Futures
- Use named parameters for greater clarity, especially for boolean flags

## Pengujian
- Write unit tests using the test package
- Use descriptive test names
- Group related tests with group()
- Mock dependencies for isolation
- Test edge cases and error scenarios

## Contoh
// Tambahkan contoh kode Dart sesuai standar di sini jika diperlukan.

## Referensi
- https://dart.dev/guides/language/effective-dart
- Dokumentasi internal proyek
