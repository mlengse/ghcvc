# Panduan Umum Penulisan Kode Proyek

Panduan ini berlaku untuk seluruh kode yang dihasilkan oleh GitHub Copilot untuk proyek ini.

## Bahasa Default
- Gunakan Bahasa Indonesia sebagai bahasa default untuk semua interaksi
- Berikan respons dalam Bahasa Indonesia yang formal dan profesional
- Untuk istilah teknis yang tidak memiliki padanan dalam Bahasa Indonesia, gunakan istilah aslinya dengan format *italic*
- Jelaskan istilah teknis jika diperlukan untuk memastikan pemahaman yang jelas

## Gaya Komunikasi
- Gunakan kalimat yang jelas, ringkas, dan mudah dimengerti
- Berikan jawaban yang komprehensif tetapi tidak bertele-tele
- Struktur jawaban dengan baik menggunakan pemformatan yang sesuai
- Sesuaikan tingkat formalitas berdasarkan konteks

## Standar Penulisan Kode

- Gunakan kode yang bersih dan mudah dipelihara dengan komentar yang sesuai
- Ikuti praktik terbaik dan idiom khusus bahasa pemrograman yang digunakan
- Utamakan keterbacaan dan kemudahan pemeliharaan dibandingkan trik yang rumit
- Sertakan penanganan *error* yang tepat untuk semua operasi eksternal
- Gunakan penamaan variabel, fungsi, dan kelas yang bersifat semantik
- Tambahkan komentar di atas logika atau algoritma yang kompleks
- Komentar dalam kode dapat dituliskan dalam Bahasa Indonesia
- Dokumentasi kode dapat menggunakan Bahasa Indonesia
- Variabel, fungsi, dan nama kelas tetap mengikuti konvensi bahasa pemrograman
- Pesan pengguna dan elemen UI menggunakan Bahasa Indonesia

## Panduan Arsitektur

- Ikuti prinsip SOLID saat merancang kelas dan modul
- Terapkan pemisahan tanggung jawab (*separation of concerns*) yang baik
- Gunakan *design pattern* secara tepat jika dapat meningkatkan kualitas kode
- Buat komponen yang dapat digunakan kembali jika memungkinkan
- Pastikan modul memiliki keterkaitan yang longgar dan kohesi yang tinggi

## Panduan Keamanan

- Validasi seluruh input pengguna sebelum diproses
- Lakukan sanitasi data sebelum digunakan dalam *SQL query* atau output
- Jangan pernah menyimpan informasi sensitif seperti API key atau kata sandi di dalam kode
- Terapkan pemeriksaan autentikasi dan otorisasi yang tepat
- Ikuti praktik penulisan kode yang aman untuk mencegah kerentanan umum (XSS, CSRF, dll.)
- Gunakan *parameterized query* untuk operasi basis data

## Pertimbangan Performa

- Optimalkan kode untuk performa jika diperlukan
- Gunakan algoritma dan struktur data yang efisien
- Minimalkan pemanggilan ke basis data dan optimalkan *query*
- Pertimbangkan strategi *caching* untuk data yang sering diakses
- Perhatikan penggunaan memori dan potensi kebocoran memori

## Pendekatan Pengujian

- Tulis *unit test* yang komprehensif untuk seluruh fungsionalitas
- Sertakan kasus batas dan skenario *error* dalam pengujian
- Pastikan pengujian bersifat independen dan dapat diulang
- Gunakan nama pengujian yang deskriptif untuk menjelaskan apa yang diuji
- Ikuti pola AAA (Arrange, Act, Assert) dalam struktur pengujian

## Dokumentasi

- Sertakan *docstring*/komentar yang jelas untuk API publik
- Dokumentasikan parameter dan nilai kembali fungsi
- Tambahkan contoh penggunaan untuk fungsi yang kompleks
- Pastikan dokumentasi selalu diperbarui sesuai perubahan kode


## Versi dan Pembaruan
version: 1.0.0
last_updated: 2025-06-21
