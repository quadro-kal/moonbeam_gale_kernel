# COLLISION-MEDIATEK.md: Mengelola Kode "Kotor" MediaTek

File ini adalah panduan paling krusial untuk menangani *error* pada *source code proprietary* MediaTek.

## Tujuan Skill (COLLISION MEDIATEK)
Merapikan *error* C-Level (sintaks kotor, enum mismatch, implicit declaration) pada driver manajemen daya dan perangkat keras MediaTek agar lulus *compile* tanpa merusak fungsionalitas aslinya (tanpa harus melakukan *rewrite* ke standar mainline).

## Strategi Resolusi:
1. **Penanganan "Enum/Integer Mismatch" & Implicit Declaration:**
   - Pada folder seperti `drivers/misc/mediatek/base/power/cpufreq_v1`, jika *compiler* memprotes konversi antara `enum mt_cpu_dvfs_id` dan `unsigned int`, solusinya adalah **mengabaikan peringatan tersebut melalui Makefile**.
   - Hapus parameter `-Werror` (Warning as Error) dari Makefile yang berada di direktori MediaTek tersebut. Biarkan *compiler* mengeluarkan *warning*, selama fungsionalitas aslinya (yang memang jalan di perangkat) tidak disentuh.
2. **Aturan "Jangan Disentuh":**
   - **TIDAK PERLU MAINLINING ULANG.** Jangan pernah mencoba mengubah alur logika *scheduler* atau *governor* bawaan pabrik (seperti `ged`, `cm_mgr`, atau DDK Mali `mali_kbase`). Modifikasi sedikit saja berisiko menyebabkan *bootloop* atau kernel *panic* di perangkat.
   - Jika Anda menggunakan *compiler* yang tepat (lihat panduan PREPARE), *error* ini bahkan tidak akan muncul.
