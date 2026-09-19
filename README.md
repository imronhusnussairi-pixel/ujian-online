# CBT Exam Browser Wahapo

Aplikasi Android WebView yang langsung membuka `https://cbt.smkwhapo.sch.id/`.

## Fitur

- WebView khusus CBT, langsung terarah ke URL ujian
- Fullscreen (status bar & navigation bar disembunyikan)
- Orientasi terkunci **portrait**
- JavaScript aktif
- Cookie/session didukung (WebView menyimpan sesi login)
- **Safe Browsing** Google aktif (memblokir halaman phishing/malware yang dikenal)
- **HTTPS wajib** — navigasi ke http:// non-aman atau sertifikat SSL bermasalah otomatis diblokir
- Navigasi dibatasi hanya ke domain `cbt.smkwhapo.sch.id` — link ke domain lain diblokir
- Tombol Back Android: mundur di dalam riwayat WebView dulu; kalau sudah di halaman awal, muncul
  konfirmasi keluar
- **Tombol keluar terlihat** (ikon "X" di pojok kanan atas) dengan dialog konfirmasi sebelum benar-benar
  keluar aplikasi
- Dukungan upload file (`<input type="file">`), untuk unggah jawaban/scan
- Ikon aplikasi placeholder (lihat catatan di bawah)

## ⚠️ Cek dulu sebelum build: nama domain

File ini dibuat memakai domain **`cbt.smkwhapo.sch.id`** (tanpa huruf "a" setelah "smk"), sesuai yang
diminta. Kalau ternyata ini salah ketik dan domain aslinya berbeda (misalnya `smkwahapo`), edit dua baris
ini di `app/src/main/res/values/strings.xml` sebelum build:

```xml
<string name="exam_url">https://cbt.smkwhapo.sch.id/</string>
<string name="allowed_host">cbt.smkwhapo.sch.id</string>
```

## Cara mendapatkan file APK (tanpa Android Studio)

1. Buat repository baru di GitHub (atau pakai yang sudah ada).
2. Upload **seluruh isi** folder `cbt-exam-browser-wahapo` ini ke repo tersebut — termasuk folder
   `.github` yang tersembunyi (aktifkan "Show hidden items" di File Explorer / `Cmd+Shift+.` di Mac
   sebelum drag-drop, atau buat filenya manual lewat "Add file → Create new file" dengan path
   `.github/workflows/build.yml` kalau drag-drop gagal).
3. Buka tab **Actions** di repo → workflow "Build APK" otomatis jalan (±3-5 menit).
4. Setelah selesai (centang hijau ✅), buka run tersebut → scroll ke bagian **Artifacts** →
   download `cbt-exam-browser-wahapo-debug-apk` → ekstrak → dapat `app-debug.apk`.
5. Pindahkan ke HP Android, buka filenya, izinkan instal dari sumber tidak dikenal jika diminta,
   lalu install.

## Yang sebaiknya dikembangkan lanjut

1. **Logo asli** — ganti `app/src/main/res/drawable/ic_launcher.xml` dengan logo sekolah yang
   sesungguhnya (lewat Image Asset Studio di Android Studio untuk hasil adaptive-icon yang rapi).
2. **Build release + signing** — versi debug cukup untuk uji coba; untuk dibagikan ke banyak HP
   siswa, build varian **release** yang ditandatangani (lebih stabil, tanpa watermark debug).
3. **Perkuat kontrol keluar** — saat ini tombol keluar bisa dipakai siapa saja (sesuai permintaan).
   Kalau nanti perlu mencegah siswa keluar sendiri saat ujian berlangsung, tombol ini bisa ditambah
   PIN admin atau diganti mode kiosk penuh (screen pinning / device-owner) seperti versi sebelumnya.
4. **Deteksi jaringan terputus** — tambah pengecekan koneksi otomatis & retry berkala saat sinyal
   putus di tengah ujian.
5. **Blokir notifikasi masuk** selama sesi ujian — butuh mode device-owner (Device Policy Manager).
