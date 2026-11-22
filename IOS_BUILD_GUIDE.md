# Panduan Build iOS / iPhone (SmartSchool Portal)

Aplikasi **SmartSchool Portal** dibangun menggunakan stack modern **React + Vite + Capacitor** (`@capacitor/ios` sudah terpasang di dependencies). Karena Anda sedang menggunakan **Windows**, file `.ipa` atau Xcode project iOS memerlukan lingkungan macOS atau Cloud CI/CD untuk dicompile.

Berikut adalah 2 opsi resmi & termudah untuk mem-build aplikasi ini ke iPhone:

---

## Opsi 1: Otomatis Tanpa Mac Menggunakan Cloud CI/CD (Codemagic / GitHub Actions) ⭐ *Paling Direkomendasikan*

Anda dapat menghasilkan file instalasi iPhone (`.ipa`) langsung dari cloud tanpa perlu membeli perangkat Mac.

### Menggunakan Codemagic (Sudah disediakan file `codemagic.yaml`)
Di dalam proyek ini sudah disiapkan konfigurasi [`codemagic.yaml`](file:///D:/Aplikasi%20Alp%20Android/codemagic.yaml) yang siap pakai:
1. Hubungkan repositori Git proyek Anda ke [Codemagic](https://codemagic.io/).
2. Pilih workflow **`ios-capacitor`**.
3. Klik **Start new build**.
4. Codemagic akan otomatis:
   - Menjalankan `npm run build`
   - Menginisialisasi iOS (`npx cap add ios` & `npx cap sync ios`)
   - Mengompilasi dengan Xcode di cloud Mac Mini M1
   - Menghasilkan file **`SmartSchool.ipa`** yang dapat langsung diunduh dan dipasang di iPhone atau diupload ke TestFlight / App Store.

---

## Opsi 2: Build Menggunakan Komputer Mac (Xcode)

Jika Anda memiliki akses ke Mac (atau laptop rekan tim):

1. **Copy atau Clone proyek ini ke komputer Mac.**
2. Buka terminal di Mac, masuk ke folder proyek, dan jalankan:
   ```bash
   npm install
   npm run build
   npx cap add ios
   npx cap sync ios
   ```
3. Buka proyek iOS di Xcode:
   ```bash
   npx cap open ios
   ```
4. Di dalam **Xcode**:
   - Pilih tab **Signing & Capabilities**.
   - Pada kolom **Team**, pilih Apple Developer Account Anda (atau Personal Team gratis).
   - Pastikan Bundle Identifier sesuai: `id.sch.alphabet.smartschool`.
5. **Jalankan ke iPhone:**
   - Hubungkan iPhone fisik dengan kabel USB ke Mac (atau pilih simulator iPhone di Xcode).
   - Klik tombol **Run (▶)** di pojok kiri atas Xcode.
   - Aplikasi akan langsung terpasang dan berjalan di iPhone Anda!

---

## Opsi 3: Pengujian Cepat di iPhone Tanpa Build Native (Web Preview / PWA)

Jika Anda hanya ingin melihat tampilan dan menguji fungsionalitas di iPhone saat ini juga tanpa Mac:
1. Jalankan development server di Windows Anda:
   ```bash
   npm run dev -- --host
   ```
2. Pastikan iPhone dan PC Anda terhubung ke jaringan Wi-Fi yang sama.
3. Buka browser **Safari** di iPhone, lalu masukkan alamat IP PC Anda (contoh: `http://192.168.1.10:3000`).
4. Tekan tombol **Share** di Safari, lalu pilih **"Add to Home Screen" (Tambahkan ke Layar Utama)**.
5. Aplikasi akan terbuka fullscreen layaknya aplikasi native iPhone dengan tampilan dan font Inter yang sudah presisi.
