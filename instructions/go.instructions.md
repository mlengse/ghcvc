---
applyTo: "**/*.go"
version: "1.0.0"
last_updated: "2025-07-03"
---

# Go Style Guide

## Ruang Lingkup
Instruksi ini berlaku untuk seluruh kode Go di proyek.

## Standar Penamaan
- Gunakan MixedCaps (camelCase) untuk nama yang diekspor
- Gunakan mixedCaps untuk nama yang tidak diekspor
- Singkatan harus ditulis dengan huruf kapital semua (misalnya, HTTP, URL, ID)
- Nama antarmuka sering diakhiri dengan -er (misalnya, Reader, Writer)

## Format dan Gaya
- Gunakan gofmt untuk pemformatan otomatis
- Indentasi dengan tab, bukan spasi
- Panjang baris sebaiknya kurang dari 120 karakter
- Kelompokkan deklarasi yang terkait
- Tambahkan baris kosong antar definisi fungsi

## Praktik Terbaik
- Ikuti Go Proverbs (https://go-proverbs.github.io/)
- Utamakan komposisi daripada pewarisan
- Gunakan antarmuka untuk decoupling
- Buat nilai nol berguna
- Gunakan context.Context untuk pembatalan, batas waktu, dan meneruskan nilai yang terkait dengan permintaan
- Gunakan goroutine dan saluran dengan tepat
- Hindari variabel global
- Laksanakan pembersihan sumber daya yang tepat dengan defer

### Konkruensi
- Gunakan goroutine untuk operasi bersamaan
- Gunakan saluran untuk komunikasi antar goroutine
- Pertimbangkan primitif sinkronisasi (Mutex, RWMutex) untuk keadaan bersama yang sederhana
- Hindari balapan data dengan sinkronisasi yang tepat
- Berhati-hatilah dengan kebocoran goroutine
- Gunakan konteks untuk pembatalan

## Penanganan Kesalahan
- Periksa kesalahan secara eksplisit; jangan gunakan pola try-catch
- Kembalikan kesalahan daripada menggunakan pengecualian
- Gunakan fmt.Errorf untuk memformat pesan kesalahan
- Buat tipe kesalahan kustom untuk kasus kesalahan tertentu jika diperlukan
- Pertimbangkan untuk menggunakan errors.Is() dan errors.As() untuk inspeksi kesalahan

## Pengujian
- Tulis pengujian yang dipimpin tabel
- Gunakan subtes untuk mengatur kasus uji
- Gunakan t.Helper() untuk fungsi pembantu
- Manfaatkan fitur bawaan go test seperti cakupan pengujian
- Gunakan testify atau pustaka pernyataan lainnya dengan hemat
- Pertimbangkan pengujian kinerja untuk kode yang krusial secara kinerja
- Gunakan contoh yang berfungsi sebagai dokumentasi

## Contoh
Tambahkan contoh kode Go sesuai standar di sini jika diperlukan. Misal:

```go
func ExampleAdd() {
    got := Add(1, 2)
    fmt.Println(got)
    // Output: 3
}
```

## Referensi
- https://golang.org/doc/effective_go.html
- https://go-proverbs.github.io/
