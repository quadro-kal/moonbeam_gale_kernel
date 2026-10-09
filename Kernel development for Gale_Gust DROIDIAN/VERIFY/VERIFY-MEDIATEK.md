# VERIFY-MEDIATEK.md: Verifikasi Fungsionalitas Hardware MediaTek

File ini berfokus pada pengecekan *hardware* saat perangkat sudah berhasil menyala (booting) menggunakan kernel baru ini.

## Tujuan Skill (VERIFY MEDIATEK)
Memastikan bahwa *proprietary hardware* perangkat (Redmi 13C/POCO C65) berfungsi sempurna tanpa adanya regresi atau kerusakan.

## Langkah Pengecekan Hardware:
1. **Layar & Grafis (DRM/KMS):**
   - Pastikan layar tidak hitam (*black screen*) setelah logo boot.
   - Karena Droidian menggunakan antarmuka grafis (seperti Phosh), pastikan UI muncul. Jika UI muncul, periksa log dengan perintah `dmesg | grep panfrost`.
   - Pastikan Panfrost sukses melakukan inisialisasi dan memuat *Mali GPU*. Jika gagal, antarmuka grafis mungkin berjalan lambat (hanya *software rendering*).
2. **Konektivitas Dasar:**
   - Lakukan pengecekan via `dmesg` atau terminal Droidian:
     - Apakah Modem/Sinyal terbaca via *Ofono*?
     - Apakah Wi-Fi (*wmt_wifi*) bisa dinyalakan?
3. **Manajemen Daya:**
   - Biarkan ponsel menyala beberapa saat. Cek apakah perangkat menjadi sangat panas atau *restart* sendiri secara tiba-tiba (*Kernel Panic*). Jika iya, artinya ada modul MediaTek (seperti CPUFreq/GED) yang tidak terkonfigurasi dengan benar saat kompilasi.
