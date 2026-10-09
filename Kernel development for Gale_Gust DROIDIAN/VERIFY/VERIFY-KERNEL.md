# VERIFY-KERNEL.md: Verifikasi Output Kernel

File ini berisi panduan setelah kernel selesai di-compile, untuk memastikan kernel tersebut valid dan siap diinstal.

## Tujuan Skill (VERIFY KERNEL)
Mengecek secara fisik dan struktural bahwa hasil akhir (*binary*) kernel memiliki semua modul dan konfigurasi yang tepat sebelum perangkat di-*flash*.

## Langkah Verifikasi:
1. **Pengecekan File Binary:**
   - Periksa ketersediaan file `arch/arm64/boot/Image.gz` atau `Image.gz-dtb`. Ini adalah jantung sistem Anda.
2. **Pengecekan Log Kompilasi:**
   - Pastikan bahwa driver Panfrost (`panfrost.ko` atau *built-in* objek `panfrost_drv.o`) benar-benar ikut ter-*link* ke dalam kernel (cek output dari proses tautan *vmlinux*).
3. **Penyatuan dengan Boot Image:**
   - Gunakan *Android Image Kitchen* atau alat serupa untuk mengemas ulang (`repack`) `Image.gz` ini menjadi `boot.img` Android.
   - Anda perlu menggunakan `ramdisk` dari proyek Droidian/Halium agar proses *init* langsung melompat ke rootfs Linux, bukan ke *userland* Android biasa.
