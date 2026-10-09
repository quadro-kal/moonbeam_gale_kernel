# PREPARE-KERNEL.md: Tujuan & Persiapan Dasar Kernel

File ini berisi panduan untuk mempersiapkan *source code* kernel dasar sebelum kita memulai integrasi Droidian dan Halium.

## Tujuan Skill (PREPARE KERNEL)
Tujuan utama di tahap ini adalah memastikan Anda memiliki basis kode (baseline) yang bersih dari repositori kernel bawaan perangkat Gale/Gust (Redmi 13C/POCO C65), serta mempersiapkan *toolchain* (compiler) yang tepat agar proses kompilasi berjalan tanpa hambatan.

## Langkah-langkah Persiapan:
1. **Pilih Compiler (Toolchain) yang Tepat:**
   - Karena kernel ini berbasis Linux 4.19, **JANGAN** menggunakan GCC 13+ atau Clang 16+.
   - Sangat disarankan untuk menggunakan **Proton Clang 13** atau *AOSP Clang/GCC* (misal GCC 4.9) yang kompatibel dengan kode pabrikan (MediaTek). Penggunaan *compiler* modern akan memicu ribuan *error* kompilasi pada kode *power management* (cpufreq, cm_mgr).
2. **Setup Source Code Halium/Droidian:**
   - Pahami daftar fitur yang wajib aktif (sudah ditambahkan ke `gale_defconfig`), seperti:
     - `CONFIG_ANDROID_BINDERFS=y`
     - `CONFIG_NAMESPACES=y`
     - `CONFIG_OVERLAY_FS=y`
     - `CONFIG_SECURITY_APPARMOR=y`
3. **Persiapan Patch Halium 13:**
   - Kumpulkan *patchset* Halium 13 dari repositori Halium (seperti `halium-9.0` atau cabang `halium-13` jika ada) yang berkaitan dengan fungsionalitas Android 13.
