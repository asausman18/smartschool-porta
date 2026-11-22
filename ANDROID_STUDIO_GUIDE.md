# Panduan Lengkap: Memindahkan Aplikasi SmartSchool ke Android Studio (Tampilan 100% Sama Tanpa Berubah)

Dokumen ini menjelaskan secara tuntas bagaimana cara membuka, menjalankan, dan mengekspor proyek **SmartSchool** ini ke dalam **Android Studio** tanpa merubah tampilan antarmuka (UI), warna, font, maupun animasi sedikitpun.

---

## 💡 Mengapa Tampilannya Dijamin 100% Sama Persis?

Aplikasi ini menggunakan **Capacitor (by Ionic)** yang membungkus kode React + Vite + Tailwind CSS ke dalam proyek native Android resmi.

- **Chromium WebView Modern**: Android Studio akan merender aplikasi ini menggunakan mesin WebView Android bawaan (Chromium) yang mendukung 100% CSS modern, Flexbox, CSS Grid, animasi Tailwind, font *Plus Jakarta Sans*, transisi *Motion*, hingga modal dialog interaktif.
- **Bukan Konversi Manual**: Anda **TIDAK PERLU** menulis ulang tampilan ke XML Android atau Jetpack Compose.
- **Satu Sumber Kode**: Apa yang Anda lihat di browser atau emulator HP, persis sama 100% ketika dijalankan di HP Android fisik (Samsung, Xiaomi, Oppo, Vivo, dsb).

Folder native Android (`/android`) **sudah berhasil dibuat dan dikonfigurasi** di proyek ini lengkap dengan Gradle, AndroidManifest, dan aset produksinya!

---

## 🚀 Cara 1: Menggunakan Capacitor (Metode Resmi & Paling Mudah - Rekomendasi)

### Langkah 1: Unduh / Clone Proyek ke Komputer / Laptop Anda
Pastikan laptop Anda sudah terinstall:
- **Node.js** (versi 18 atau 20+)
- **Android Studio** (versi Flamingo, Hedgehog, Iguana, Koala, atau yang lebih baru)

### Langkah 2: Buka Proyek di Android Studio
Ada dua cara mudah untuk membukanya:

#### Opsi A: Lewat Terminal (Paling Cepat)
Buka terminal / Command Prompt di folder proyek ini, lalu ketik:
```bash
npx cap open android
```
Android Studio akan otomatis terbuka dan memuat folder `android/`.

#### Opsi B: Lewat Menu Android Studio Langsung
1. Buka aplikasi **Android Studio**.
2. Di layar sambutan, pilih **Open** (atau jika sudah terbuka, klik menu **File > Open...**).
3. Arahkan dan pilih folder **`android`** yang ada di dalam proyek ini (bukan folder root, melainkan sub-folder bernama `android`).
4. Klik **OK** / **Open**.

---

### Langkah 3: Tunggu Gradle Sync Selesai
1. Ketika pertama kali membuka, Android Studio akan otomatis mengunduh dependensi Gradle (progress bar terlihat di pojok kanan bawah).
2. Tunggu 1 - 3 menit sampai proses Gradle selesai dan muncul tanda centang hijau.

---

### Langkah 4: Jalankan di HP Fisik atau Emulator (Tampilan 100% Persis)
1. **Menggunakan HP Android Asli**:
   - Aktifkan *Developer Options* & *USB Debugging* di HP Anda.
   - Hubungkan HP ke laptop menggunakan kabel USB.
   - Di toolbar atas Android Studio, pilih nama HP Anda.
   - Klik tombol **Run (Ikon Segitiga Hijau ▶)** atau tekan `Shift + F10`.
2. **Menggunakan Emulator**:
   - Klik icon *Device Manager* di Android Studio > Buat Virtual Device (misal: Pixel 7).
   - Klik tombol **Run (▶)**.

Aplikasi SmartSchool akan langsung terinstall di HP dengan tampilan biru-kuning, saldo jajan, QR kantin, absensi, dan buku penghubung persis sama seperti desain web!

---

## 🔄 Bagaimana Jika Anda Mengubah Tampilan atau Kode di React?

Jika di kemudian hari Anda mengedit kode di folder `src/` (misalnya mengganti warna, menambah menu, atau mengubah teks):

Cukup jalankan 2 perintah ini di terminal:
```bash
# 1. Compile kode web terbaru
npm run build

# 2. Sinkronkan file terbaru ke dalam folder Android Studio
npx cap sync
```

Setelah itu, kembali ke Android Studio dan klik tombol **Run (▶)** lagi. Perubahan Anda akan langsung terupdate ke HP Android!

---

## 📦 Cara Menghasilkan File APK (Untuk Dibagikan ke Guru / Orang Tua via WhatsApp)

Jika Anda ingin membagikan file APK langsung tanpa lewat Play Store:
1. Di Android Studio, klik menu bar atas: **Build** > **Build Bundle(s) / APK(s)** > **Build APK(s)**.
2. Tunggu 1 menit hingga muncul notifikasi di pojok kanan bawah:
   *"APK(s) generated successfully for 1 module"*.
3. Klik tulisan **locate**.
4. Anda akan menemukan file:
   `android/app/build/outputs/apk/debug/app-debug.apk`.
5. File `.apk` ini bisa langsung Anda kirim lewat WhatsApp atau Google Drive ke siapa saja untuk di-install di HP Android mereka!

---

## 🌐 Cara Menghasilkan File AAB (Untuk Google Play Store Resmi)

Google Play Store mewajibkan format **.aab** yang ditandatangani secara digital (Signed):

1. Di Android Studio, klik menu: **Build** > **Generate Signed Bundle / APK...**
2. Pilih opsi **Android App Bundle (.aab)** > Klik **Next**.
3. Di bagian **Key store path**:
   - Klik **Create new...** jika belum pernah membuat kunci.
   - Tentukan lokasi penyimpanan file (misal: `smartschool-key.jks`).
   - Masukkan password, alias (`smartschool`), dan nama sekolah Anda.
   - Klik **OK**.
4. Pilih Build Variant: **release** (jangan pilih debug).
5. Klik **Finish**.
6. Setelah selesai, klik tulisan **locate** untuk mendapatkan file:
   `android/app/release/app-release.aab`.
7. Upload file `.aab` ini ke akun Google Play Console Anda.

---

## 🛠️ Cara 2: Alternatif Native Android WebView (Murni Android Studio Tanpa Node.js di Studio)

Jika Anda ingin proyek Android murni yang berdiri sendiri tanpa dependensi Capacitor:

1. Jalankan build di proyek web ini:
   ```bash
   npm run build
   ```
   Ini akan menghasilkan folder `dist/` yang berisi `index.html` dan folder `assets/`.

2. Buka **Android Studio** > Buat proyek baru (**New Project**) > Pilih template **Empty Views Activity** (Kotlin atau Java).
3. Di dalam proyek Android Studio baru tersebut:
   - Buat folder aset di: `app/src/main/assets/`
   - Salin seluruh isi folder `dist/*` dari proyek web ke dalam `app/src/main/assets/` (sehingga ada `app/src/main/assets/index.html`).
4. Buka file `app/src/main/res/layout/activity_main.xml`, ganti isinya dengan WebView satu layar penuh:
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <WebView xmlns:android="http://schemas.android.com/apk/res/android"
       android:id="@+id/webView"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```
5. Buka `MainActivity.kt`, aktifkan JavaScript dan muat file aset:
   ```kotlin
   package id.sch.alphabet.smartschool

   import android.annotation.SuppressLint
   import android.os.Bundle
   import android.webkit.WebSettings
   import android.webkit.WebView
   import android.webkit.WebViewClient
   import androidx.appcompat.app.AppCompatActivity

   class MainActivity : AppCompatActivity() {
       @SuppressLint("SetJavaScriptEnabled")
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)

           val webView = findViewById<WebView>(R.id.webView)
           webView.webViewClient = WebViewClient()
           
           val webSettings = webView.settings
           webSettings.javaScriptEnabled = true
           webSettings.domStorageEnabled = true
           webSettings.databaseEnabled = true
           webSettings.allowFileAccess = true
           webSettings.loadWithOverviewMode = true
           webSettings.useWideViewPort = true

           // Muat halaman utama aplikasi
           webView.loadUrl("file:///android_asset/index.html")
       }
   }
   ```
6. Tambahkan izin internet di `AndroidManifest.xml` (di dalam tag `<manifest>`):
   ```xml
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   ```

Tampilan aplikasi akan 100% sama persis karena WebView Android membaca file HTML, Tailwind CSS, font, dan animasi yang identik!

---

## 📋 Ringkasan File Konfigurasi yang Tersedia di Proyek Ini

1. **`/capacitor.config.ts`**: Konfigurasi nama aplikasi, ID paket Android (`id.sch.alphabet.smartschool`), skema HTTPS, dan warna background status bar `#0f172a`.
2. **`/android`**: Folder proyek Android Studio native siap pakai.
3. **`/android/app/src/main/assets/public`**: Bundle aplikasi web yang sudah ter-compile dan siap dijalankan secara offline maupun online.
