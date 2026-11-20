# Matriks Skenario dan Hasil Pengujian Proyek 6A

Matriks ini berisi dokumentasi skenario pengujian positif dan negatif pada proyek **Server Berkas Bersama dengan Backup dan Audit Akses**. Hasil pengujian disusun berdasarkan pelaksanaan pengujian yang telah dicatat dalam laporan praktikum.

## Matriks Pengujian

| ID | Penanggung Jawab | NIM | Skenario Pengujian | Jenis | Hasil Aktual | Status | Bukti |
|---|---|---|---|---|---|---|---|
| T1-P | Mario Dionisius Pake | 2510512201 | Operator membuat file pada folder share menggunakan user `op1`. | Positif | File berhasil dibuat dengan exit code 0 dan grup kepemilikan `sf_operator`. Hak akses file menunjukkan `-rw-rw----+`. | Lulus | Portofolio Pribadi/Laporan Subbab 5.2 |
| T1-N | Mario Dionisius Pake | 2510512201 | User `tamu1` mencoba melihat isi folder share. | Negatif | Akses ditolak dengan pesan `Permission denied` dan exit code 2. | Lulus | Portofolio Pribadi/Laporan Subbab 5.2 |
| T2-P | Zahara Marchela | 2510512200 | Memeriksa status layanan Samba menggunakan `systemctl`. | Positif | Layanan `smbd` berstatus `active (running)` dan `enabled`. | Lulus | Portofolio/Laporan Subbab 5.3 |
| T2-N | Zahara Marchela | 2510512200 | Memeriksa validitas konfigurasi Samba menggunakan `testparm -s`. | Negatif | `testparm` menunjukkan konfigurasi valid dan menampilkan pengaturan share `[berkas]`. Terdapat peringatan nama NetBIOS melebihi 15 karakter. | Lulus dengan catatan | Portofolio Pribadi/Laporan Subbab 5.3 |
| T3-P | Fricelmo Rikar Weohawu Thalo | 2510512192 | Client Windows terhubung ke server melalui port 445 dan membuka share menggunakan akun `op1`. | Positif | `TcpTestSucceeded` bernilai `True`, autentikasi berhasil, dan folder share dapat dibuka melalui File Explorer. | Lulus | Portofolio Pribadi/Laporan Subbab 5.4 |
| T3-N1 | Fricelmo Rikar Weohawu Thalo | 2510512192 | Client mencoba mengakses share menggunakan password yang salah. | Negatif | Autentikasi ditolak dengan `System error 86` karena password tidak benar. | Lulus | Portofolio Pribadi/Laporan Subbab 5.4 |
| T3-N2 | Fricelmo Rikar Weohawu Thalo | 2510512192 | Client mencoba membuka share tanpa kredensial yang sesuai. | Negatif | Akses tidak berhasil. Muncul pesan terkait SMB signing dan `Access is denied` setelah koneksi dihapus. | Lulus dengan catatan | Portofolio Pribadi/Laporan Subbab 5.4 |
| T4-P | Salma Kamila Arifin | 2510512191 | Reader membuka dan menyalin `t2.txt` melalui File Explorer, kemudian memeriksa checksum. | Positif | File berhasil dibaca dan disalin. Checksum sesuai dengan checksum awal server. | Lulus | Portofolio Pribadi/Laporan Subbab 5.5 |
| T4-N | Salma Kamila Arifin | 2510512191 | Reader mencoba membuat file, menghapus file, dan mengganti nama `t2.txt`. | Negatif | Ketiga operasi ditolak. File `t2.txt` tetap tersedia. | Lulus | Portofolio Pribadi/Laporan Subbab 5.5 |
| T5-P | Muhammad Ikhlas Aulya | 2510512198 | Administrator `adm1` login melalui SSH dan menjalankan perintah pemeriksaan layanan menggunakan sudo. | Positif | Login SSH berhasil, perintah pemeriksaan `smbd` berhasil dijalankan, dan exit code 0. | Lulus | Portofolio Pribadi/Laporan Subbab 5.6 |
| T5-N1 | Muhammad Ikhlas Aulya | 2510512198 | User `tamu1` mencoba login melalui SSH. | Negatif | Login ditolak dengan `Permission denied` dan exit code 255 karena user tidak termasuk `AllowGroups`. | Lulus | Portofolio Pribadi/Laporan Subbab 5.6 |
| T5-N2 | Muhammad Ikhlas Aulya | 2510512198 | User `op1` mencoba menghentikan layanan `smbd` menggunakan sudo. | Negatif | Perintah ditolak oleh kebijakan sudoers. Exit code 1 dan layanan `smbd` tetap `active`. | Lulus | Portofolio Pribadi/Laporan Subbab 5.6 |
| T6-P | Anisa Nugrahini | 2510512182 | Membuat backup, memverifikasi checksum, melakukan restore, dan membandingkan isi direktori menggunakan `diff -r`. | Positif | Backup berhasil dibuat, checksum menunjukkan `OK`, restore berhasil, dan `diff -r` menunjukkan tidak ada perbedaan dengan exit code 0. | Lulus | Portofolio Pribadi/Laporan Subbab 5.7 |
| T6-N | Anisa Nugrahini | 2510512182 | Memodifikasi satu byte pada salinan arsip backup lalu mencoba melakukan restore. | Negatif | Verifikasi checksum menunjukkan `FAILED`. Restore dibatalkan dengan exit code 5 sebelum arsip dipulihkan. | Lulus | Portofolio Pribadi/Laporan Subbab 5.7 |
| T7-P | Dimas Dwi Surya | 2510512196 | Menjalankan container Docker untuk membaca laporan melalui bind mount read-only. | Positif | Container berhasil membaca `laporan.txt` dan menampilkan isinya dengan exit code 0. | Lulus | Portofolio Pribadi/Laporan Subbab 5.8 |
| T7-N | Dimas Dwi Surya | 2510512196 | Mencoba mengubah laporan melalui container Docker dengan mount read-only. | Negatif | Penulisan ditolak dengan pesan `Read-only file system` dan exit code 1. Checksum host tetap `OK`. | Lulus | Portofolio Pribadi/Laporan Subbab 5.8 |

## Keterangan Status

- **Lulus:** Hasil aktual sesuai dengan hasil yang diharapkan.
- **Gagal:** Hasil aktual tidak sesuai dengan hasil yang diharapkan.
- **Belum Diuji:** Pengujian belum dilaksanakan.
- **Lulus dengan catatan:** Pengujian memenuhi tujuan utama, tetapi terdapat temuan yang perlu diperhatikan.
