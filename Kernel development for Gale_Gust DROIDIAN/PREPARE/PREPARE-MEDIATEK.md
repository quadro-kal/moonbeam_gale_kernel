# PREPARE-MEDIATEK.md: Persiapan Khusus Hardware MediaTek

File ini berfokus pada persiapan *driver* bawaan (downstream) MediaTek agar tidak rusak saat diintegrasikan dengan Droidian.

## Tujuan Skill (PREPARE MEDIATEK)
Memastikan seluruh struktur *proprietary driver* MediaTek (Kamera, Modem, Layar/DRM, Baterai, dan CPUFreq) siap untuk dikompilasi bersamaan dengan komponen Linux Userland tanpa mengganggu fungsionalitas aslinya.

## Langkah-langkah Persiapan:
1. **Identifikasi Driver Kritis:**
   - Layar: `drivers/misc/mediatek/video/`
   - Grafis (Bifrost DDK): `drivers/gpu/mediatek/gpu_mali/`
   - Manajemen Daya: `drivers/misc/mediatek/base/power/`
2. **Isolasi Kode Terhadap Compiler:**
   - Tandai direktori MediaTek yang rawan *error* kompilasi. Jika menggunakan *toolchain* yang sedikit lebih baru, siapkan strategi untuk menonaktifkan *warning as error* (`-Werror`) di Makefile pada direktori `cpufreq_v1`, `cm_mgr_v1`, dll.
3. **Persiapan Libhybris:**
   - Pahami bahwa driver MediaTek tidak berjalan murni secara *native* di Linux (X11/Wayland), melainkan harus melalui jembatan **libhybris**. Siapkan konfigurasi Android (`system.prop`, `vendor` tree) yang cocok dengan versi Halium 13 untuk diekstraksi ke *rootfs* Droidian nanti.
