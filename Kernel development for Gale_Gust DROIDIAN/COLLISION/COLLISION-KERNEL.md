# COLLISION-KERNEL.md: Penggabungan & Resolusi Konflik Halium/Kernel

File ini membahas strategi penggabungan antara kode kernel *downstream* bawaan dengan fitur Halium 13 dan komponen modern lainnya.

## Tujuan Skill (COLLISION KERNEL)
Tujuan di tahap ini adalah untuk menggabungkan dua entitas yang berbeda (Kernel Android vs Patch Halium/Mainline) dan merapikan potensi konflik struktur tanpa perlu melakukan proses *mainlining* (menulis ulang dari nol) yang memakan waktu.

## Panduan Penggabungan:
1. **Penerapan Patch Halium 13:**
   - Gunakan `patch -p1 < [nama-patch]` untuk menerapkan patch fungsionalitas Android 13 (seperti perbaikan binderfs atau ashmem).
   - Jika terjadi `reject` (file `.rej`), buka file tujuan dan gabungkan (*merge*) secara manual dengan mencari blok fungsi yang mirip. Kode *downstream* 4.19 biasanya memiliki modifikasi dari MediaTek yang menggeser baris kode asli.
2. **Harmonisasi Panfrost & DRM:**
   - Saat memasukkan driver GPU Panfrost (di-backport dari kernel terbaru), akan ada *API mismatch* pada subsistem DRM (misal: `drm_gem_object_lookup`, `dma_resv`).
   - Ubah/sesuaikan argumen pemanggilan fungsi Panfrost agar cocok dengan versi fungsi DRM yang ada di kernel 4.19. **Jangan** mengganti keseluruhan subsistem DRM 4.19, karena akan merusak driver layar MediaTek (`mtk_disp`).
