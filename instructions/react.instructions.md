---
applyTo: "**/*.jsx,**/*.tsx,**/*react*/**"
version: "1.0.0"
last_updated: "2025-07-03"
---
# React Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode React di proyek.

## Standar Penamaan
- PascalCase untuk komponen
- camelCase untuk instance dan props
- Nama file/deskripsi konsisten

## Format dan Gaya
- Komponen fungsional dengan hooks
- Komponen kecil dan fokus
- Satu file per komponen
- Group komponen terkait
- Prop destructuring
- PropTypes/TypeScript untuk tipe
- Default value untuk props opsional
- Hindari prop drilling berlebih
- Gunakan spread props dengan bijak
- Callback sebagai props, hindari inline function
- State lokal, gunakan Context/Redux untuk global
- useMemo/useCallback untuk optimasi
- Styling konsisten (CSS Modules, Styled Components, dsb)
- Responsif dan aksesibel
- React.memo untuk komponen pure
- Virtualisasi list panjang
- Lazy load dan code splitting
- Key di list
- Fragment untuk DOM minimal
- Error Boundary untuk error
- Portal untuk modal/overlay
- Form handling terstandar

## Praktik Terbaik
- Ikuti Rules of Hooks
- Custom hook untuk logic reuse
- Nama hook dengan "use"
- useEffect untuk side effect
- Dependency array benar
- Accessibility (HTML semantik, ARIA)

## Pengujian
- React Testing Library untuk unit test
- Test perilaku, bukan implementasi
- Mock dependency eksternal
- Test interaksi user
- Integration test untuk flow penting

## Contoh
Tambahkan contoh kode React sesuai standar di sini jika diperlukan.

## Referensi
- https://react.dev/learn
- https://react.dev/reference
