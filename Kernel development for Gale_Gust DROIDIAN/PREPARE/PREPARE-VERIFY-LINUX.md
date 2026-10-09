# PREPARE-VERIFY-LINUX.md: Verifikasi Persiapan Linux Userland

File ini digunakan untuk mengecek kelengkapan pra-syarat sistem GNU/Linux modern sebelum melakukan penggabungan kode (Collision).

## Tujuan Skill (PREPARE VERIFY LINUX)
Memastikan bahwa kernel memiliki seluruh kerangka dasar yang diwajibkan oleh Systemd, LXC (Linux Containers), dan Wayland (untuk Phosh/UI Droidian).

## Ceklist Persiapan:
1. **Container & Systemd Check:**
   - Pastikan konfigurasi `Cgroups` (termasuk `CGROUP_FREEZER`, `CGROUP_DEVICE`, `MEMCG`) sudah terdaftar.
   - Namespaces (`USER_NS`, `PID_NS`, `NET_NS`) harus dipersiapkan agar LXC yang menjalankan layanan Android dapat menyala di dalam Droidian.
2. **Security Check:**
   - Persiapkan *AppArmor*. Droidian sangat ketat mengenai keamanan container.
3. **Persiapan Panfrost (GPU):**
   - Pastikan struktur direktori `drivers/gpu/drm/panfrost` dan dependensinya (`drm/scheduler`) telah ada di dalam *tree* dan masuk ke dalam skema *Kconfig* utama. Panfrost akan bertindak sebagai penggerak antarmuka (UI) Droidian secara hardware-accelerated.
