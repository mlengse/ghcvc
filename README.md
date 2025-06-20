# Kustomisasi GitHub Copilot

Repository ini berisi konfigurasi kustomisasi GitHub Copilot untuk meningkatkan pengalaman pengembangan dengan menggunakan AI. Kustomisasi ini membantu memastikan hasil dan interaksi dengan Copilot sesuai dengan standar kode, arsitektur, dan praktik terbaik proyek.

## 📋 Daftar Isi

- [Struktur Repository](#struktur-repository)
- [Instruksi Kustomisasi](#instruksi-kustomisasi)
- [Mode Chat Kustom](#mode-chat-kustom)
- [Prompt Kustom](#prompt-kustom)
- [Konfigurasi CODEOWNERS](#konfigurasi-codeowners)
- [Cara Penggunaan](#cara-penggunaan)
- [Kontribusi](#kontribusi)
- [Penggunaan Sebagai Submodule](#penggunaan-sebagai-submodule)

## 🗂️ Struktur Repository

```
.github/
├── CODEOWNERS                         # Konfigurasi kepemilikan kode GitHub
├── copilot-instructions.md            # Instruksi utama Copilot untuk seluruh proyek
├── chatmodes/                         # Mode chat kustom untuk konteks berbeda
│   ├── planning.chatmode.md           # Mode perencanaan untuk arsitektur dan desain
│   ├── development.chatmode.md        # Mode pengembangan untuk implementasi
│   ├── code-review.chatmode.md        # Mode review untuk tinjauan kode
│   ├── repo-custom.chatmode.md        # Mode untuk membuat konfigurasi Copilot
│   └── bahasa-indonesia.chatmode.md   # Mode untuk interaksi dalam Bahasa Indonesia
├── instructions/                      # Instruksi khusus bahasa dan spesialisasi
│   ├── javascript.instructions.md     # Standar kode JavaScript/TypeScript
│   ├── python.instructions.md         # Standar kode Python
│   ├── java.instructions.md           # Standar kode Java
│   ├── go.instructions.md             # Standar kode Go
│   ├── dart.instructions.md           # Standar kode Dart
│   ├── flutter.instructions.md        # Standar kode Flutter
│   ├── react.instructions.md          # Standar kode React
│   ├── nextjs.instructions.md         # Standar kode Next.js
│   ├── rust.instructions.md           # Standar kode Rust
│   ├── kotlin.instructions.md         # Standar kode Kotlin
│   ├── agent-mode.instructions.md     # Instruksi khusus mode agen
│   └── bahasa-indonesia.instructions.md # Instruksi untuk interaksi Bahasa Indonesia
└── prompts/                           # Template prompt yang dapat digunakan kembali
    ├── generate-tests.prompt.md       # Template untuk membuat unit test
    ├── security-review.prompt.md      # Template untuk review keamanan kode
    ├── create-api-endpoint.prompt.md  # Template untuk membuat endpoint API
    ├── generate-documentation.prompt.md # Template untuk membuat dokumentasi
    ├── analyze-repo-generate-instructions.prompt.md # Analisis repo & buat instruksi
    ├── create-custom-chatmode.prompt.md # Buat mode chat kustom
    ├── create-custom-prompt.prompt.md # Buat prompt kustom
    ├── generate-architecture-instructions.prompt.md # Buat instruksi arsitektur
    ├── dokumentasi-indonesia.prompt.md # Buat dokumentasi dalam Bahasa Indonesia
    ├── terjemahan-error.prompt.md     # Terjemahkan pesan error ke Bahasa Indonesia
    └── review-kode-indonesia.prompt.md # Review kode dengan komentar Bahasa Indonesia

.vscode/
├── settings.json                      # Template konfigurasi VSCode untuk GitHub Copilot
└── README.md                          # Dokumentasi konfigurasi VSCode

.gitignore.template                    # Template .gitignore untuk berbagai bahasa
```

## 📝 Instruksi Kustomisasi

Repository ini berisi beberapa jenis file instruksi untuk GitHub Copilot:

1. **Instruksi Umum Proyek** (`copilot-instructions.md`): Standar kode dan pedoman umum yang berlaku untuk seluruh kode yang dihasilkan.

2. **Instruksi Khusus Bahasa** (`instructions/`): Standar kode yang disesuaikan untuk JavaScript/TypeScript, Python, Java, Go, Dart, Flutter, React, Next.js, Rust, dan Kotlin, yang akan diterapkan secara otomatis saat bekerja dengan file-file dari jenis tersebut.

3. **Instruksi Mode Agen** (`agent-mode.instructions.md`): Instruksi khusus untuk saat Copilot beroperasi dalam mode agen otonom.

4. **Instruksi Bahasa Indonesia** (`bahasa-indonesia.instructions.md`): Memastikan semua interaksi dengan pengguna menggunakan Bahasa Indonesia yang benar dan jelas.

## 💬 Mode Chat Kustom

Repository ini menyediakan mode chat khusus untuk aktivitas pengembangan yang berbeda:

1. **Planning Mode**: Untuk diskusi arsitektur dan desain, fokus pada perencanaan tingkat tinggi.

2. **Development Mode**: Untuk implementasi fitur dan penulisan kode, fokus pada menghasilkan kode yang mengikuti standar proyek.

3. **Code Review Mode**: Untuk tinjauan kode dan peningkatan kualitas, fokus pada menemukan bug dan masalah keamanan.

4. **Repo Customization Mode**: Untuk menganalisis struktur repository dan menghasilkan konfigurasi Copilot yang sesuai.

5. **Mode Bahasa Indonesia**: Mode khusus untuk memastikan semua interaksi menggunakan Bahasa Indonesia.

## 🔍 Prompt Kustom

Repository ini menyediakan template prompt yang dapat digunakan kembali untuk tugas-tugas umum:

1. **Generate Tests**: Template untuk membuat unit test yang komprehensif.

2. **Security Review**: Template untuk melakukan review keamanan kode.

3. **Create API Endpoint**: Template untuk membuat endpoint API baru.

4. **Generate Documentation**: Template untuk membuat dokumentasi kode.

5. **Analisis Repository**: Prompt untuk menganalisis repo dan membuat instruksi kustomisasi.

6. **Custom Config Creation**: Prompt untuk membuat mode chat, prompt, dan instruksi kustom.

7. **Prompt Bahasa Indonesia**: Template untuk dokumentasi, terjemahan error, dan review kode dalam Bahasa Indonesia.

## 👥 Konfigurasi CODEOWNERS

File `CODEOWNERS` mendefinisikan siapa yang bertanggung jawab untuk bagian kode yang berbeda di repository. Struktur kepemilikan kode:

- **@mlengse**: Pemilik default untuk seluruh repository dan file konfigurasi
- **@frontend-team**: Kode front-end (JS, TS, CSS, HTML)
- **@backend-team**: Kode back-end (Python, Java, Go)
- **@database-team**: File terkait database (SQL, migrasi)
- **@documentation-team**: Dokumentasi (file Markdown)
- **@qa-team**: Test (file test)
- **@security-team**: Area sensitif keamanan
- **@devops-team**: File paket dan dependensi

## 🚀 Cara Penggunaan

### Instruksi Kustom

Instruksi ini secara otomatis diterapkan saat menghasilkan kode pada file yang sesuai:

1. Instruksi umum di `copilot-instructions.md` diterapkan ke seluruh proyek
2. Instruksi bahasa khusus diterapkan berdasarkan ekstensi file
3. Instruksi mode agen diterapkan saat menggunakan mode agen

### Mode Chat

1. Pilih mode chat dari dropdown di tampilan Copilot Chat
2. Gunakan mode yang sesuai dengan jenis tugas Anda:
   - Mode Planning untuk arsitektur dan desain
   - Mode Development untuk implementasi
   - Mode Code Review untuk review kode
   - Mode Bahasa Indonesia untuk komunikasi dalam Bahasa Indonesia

### Prompt

1. Gunakan prompt dengan mengetik `/` diikuti nama prompt di input chat (misalnya, `/generate-tests`)
2. Atau pilih "Chat: Run Prompt" dari Command Palette (⇧⌘P / Ctrl+Shift+P)
3. Pilih prompt yang sesuai dengan kebutuhan Anda

### CODEOWNERS

File CODEOWNERS digunakan oleh GitHub untuk secara otomatis meminta review dari anggota tim yang tepat saat perubahan dilakukan pada bagian kode tertentu.

## 🤝 Kontribusi

Kontribusi untuk meningkatkan kustomisasi Copilot ini sangat diterima:

1. **Menambahkan instruksi bahasa baru**: Buat file di `.github/instructions/` menggunakan format yang sama
2. **Menambahkan mode chat baru**: Buat file di `.github/chatmodes/` untuk skenario khusus
3. **Menambahkan prompt baru**: Buat template di `.github/prompts/` untuk tugas berulang
4. **Memperbaiki instruksi yang ada**: Perbarui instruksi yang sudah ada untuk meningkatkan output Copilot

---

Dibuat dan dikelola oleh @mlengse dan tim. Untuk pertanyaan atau dukungan lebih lanjut, silakan buat issue dalam repository ini.

## 📦 Penggunaan Sebagai Submodule

Repository ini dapat digunakan sebagai submodule Git untuk menerapkan kustomisasi GitHub Copilot di proyek Anda. Berikut langkah-langkahnya:

1. **Tambahkan repository ini sebagai submodule Git**:

```bash
git submodule add https://github.com/mlengse/ghcvc.git .github
```

2. **Atau jika Anda sudah memiliki folder `.github`**:

```bash
git submodule add https://github.com/mlengse/ghcvc.git .github/copilot
```

3. **Perbarui dan inisialisasi submodule**:

```bash
git submodule update --init --recursive
```

### Contoh File `.gitmodules`

Berikut adalah contoh file `.gitmodules` yang akan dibuat otomatis setelah menambahkan repository ini sebagai submodule:

```
[submodule ".github"]
    path = .github
    url = https://github.com/mlengse/ghcvc.git
    branch = main
```

Atau jika ditambahkan ke folder `.github/copilot`:

```
[submodule ".github/copilot"]
    path = .github/copilot
    url = https://github.com/mlengse/ghcvc.git
    branch = main
```

### Update Submodule

Untuk memperbarui submodule ke versi terbaru:

```bash
git submodule update --remote --merge
```

### Konfigurasi VSCode (Opsional)

Repository ini juga menyediakan template konfigurasi VSCode yang dioptimalkan untuk GitHub Copilot di `.vscode/settings.json`. File ini berisi:

- **Konfigurasi GitHub Copilot**: Pengaturan optimal untuk fitur AI dan chat
- **Editor Settings**: Konfigurasi untuk pengalaman coding yang lebih baik
- **Code Quality**: Auto-formatting dan code actions on save
- **File Associations**: Asosiasi file untuk instruksi, prompt, dan chatmode Copilot
- **Language Specific**: Pengaturan khusus untuk berbagai bahasa pemrograman
- **Git Integration**: Integrasi Git yang lebih baik
- **Terminal Configuration**: Pengaturan terminal terintegrasi

Untuk menggunakan konfigurasi ini:

1. **Jika menggunakan sebagai submodule di `.github`**:
   ```bash
   cp .github/.vscode/settings.json .vscode/settings.json
   ```

2. **Jika menggunakan sebagai submodule di `.github/copilot`**:
   ```bash
   cp .github/copilot/.vscode/settings.json .vscode/settings.json
   ```

3. **Atau copy manual**: Salin isi file `.vscode/settings.json` dari repository ini ke file VSCode settings proyek Anda.

### Template .gitignore

Repository ini juga menyediakan template `.gitignore.template` yang komprehensif untuk berbagai bahasa dan framework:

- **Multi-language Support**: Mencakup JavaScript/Node.js, Python, Java, Go, Rust, Flutter/Dart
- **IDE Files**: Mengecualikan file VSCode, IntelliJ IDEA, dan editor lainnya
- **Build Artifacts**: Mengecualikan folder build, dist, dan file yang dihasilkan
- **Environment Files**: Mengecualikan file `.env` dan konfigurasi lokal
- **OS Files**: Mengecualikan file sistem seperti `.DS_Store`, `Thumbs.db`

Untuk menggunakan template ini:

```bash
# Copy template sebagai .gitignore
cp .gitignore.template .gitignore

# Atau jika menggunakan submodule
cp .github/.gitignore.template .gitignore
```

---
