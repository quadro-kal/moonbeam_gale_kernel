# VERYFY-LINUX.md: Verifikasi Lingkungan Linux (Droidian)

File ini berfokus pada pengecekan fitur-fitur Linux modern di dalam sistem Droidian yang telah menyala.

## Tujuan Skill (VERIFY LINUX)
Mengecek ketersediaan fitur kernel Linux esensial, stabilitas OS, serta kinerja containerisasi (LXC) dan sistem.

## Ceklist Verifikasi Linux:
1. **Layanan Systemd:**
   - Buka terminal (via SSH atau aplikasi terminal bawaan).
   - Jalankan `systemctl status`. Pastikan tidak ada kegagalan (*failed state*) pada unit-unit krusial (terutama layanan yang mengatur mount OverlayFS atau Halium).
2. **Container (LXC) & Jaringan Container:**
   - Droidian menjalankan Android di dalam LXC container agar bisa menggunakan driver MediaTek.
   - Cek dengan perintah `lxc-ls -f` (atau alat setara di Droidian) untuk melihat apakah container `android` berstatus *RUNNING*. Jika *STOPPED*, berarti `binderfs` atau `cgroups` belum terkonfigurasi dengan benar di kernel.
   - Cek antarmuka jaringan `waydroid0` atau `veth` menggunakan `ip a`.
3. **Penyimpanan:**
   - Cek status partisi dengan `df -h`. Pastikan ZRAM aktif menggunakan perintah `zramctl`.
   - Pastikan *AppArmor* melindungi proses-proses dengan memverifikasi profil yang dimuat via `aa-status`.
