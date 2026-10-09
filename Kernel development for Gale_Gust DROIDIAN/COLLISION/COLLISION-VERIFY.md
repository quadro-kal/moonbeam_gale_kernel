# COLLISION-VERIFY.md: Verifikasi Penggabungan

File ini berguna untuk memastikan bahwa proses penggabungan kode dan *patching* (Collision) berhasil secara struktural.

## Tujuan Skill (COLLISION VERIFY)
Mengecek apakah kernel yang telah dipatch dengan fitur Halium dan telah digabung dengan driver MediaTek dapat dikompilasi hingga menjadi file biner siap *flash* tanpa *error* fatal.

## Langkah Pengecekan:
1. **Uji Coba Kompilasi Parsial:**
   - Compile modul yang ditambahkan satu per satu terlebih dahulu (misal: `make M=drivers/gpu/drm/panfrost`). Pastikan tidak ada *fatal error* pada modul baru.
2. **Kompilasi Keseluruhan (Full Build):**
   - Jalankan `make -j$(nproc)`.
   - Pastikan *output* akhir menghasilkan file `arch/arm64/boot/Image.gz` atau `Image.gz-dtb`.
3. **Peringatan Pengecualian:**
   - Jika kompilasi terhenti karena *error* di file MediaTek (`drivers/misc/mediatek/...`), kembali baca panduan `COLLISION-MEDIATEK.md` untuk menghilangkan bendera `-Werror` atau gunakan *compiler* yang lebih lawas sesuai spesifikasi kernel 4.19 Android.
