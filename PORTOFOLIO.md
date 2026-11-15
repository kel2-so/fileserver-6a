# PORTOFOLIO KONTRIBUSI PROYEK SISTEM OPERASI

**Topik:** Server Berkas Bersama (Samba), Backup, Restore & Audit Akses

## 1. Identitas Mahasiswa

| Keterangan | Isi |
|---|---|
| Nama | Muhammad Ikhlas Aulya |
| NIM | 2510512198 |
| Kelas / Kelompok | E/Kelompok 2 |
| Mata Kuliah | Sistem Operasi |
| Tanggung Jawab | Backup, Restore, Verifikasi Checksum SHA-256, dan Sinkronisasi (flock) |
| Repository Kelompok | https://github.com/kel2-so/fileserver-6a |

## 2. Deskripsi Tanggung Jawab

Saya bertanggung jawab pada bagian Backup dan Restore dalam proyek Server Berkas Bersama. Fokus pekerjaan saya adalah mengembangkan dan mengelola proses pencadangan data (backup), verifikasi integritas arsip menggunakan checksum SHA-256, serta pemulihan data (restore).

Selain itu, saya bertanggung jawab menerapkan mekanisme sinkronisasi menggunakan perintah `flock` untuk mencegah dua proses backup berjalan secara bersamaan. Pekerjaan ini bertujuan memastikan data yang dicadangkan tetap aman, tidak mengalami kerusakan, dan dapat dipulihkan sesuai dengan data sumber.

## 3. Rincian Pekerjaan

### A. Implementasi Backup

Mengerjakan proses pencadangan data dari direktori bersama (`share/`) ke direktori penyimpanan backup (`backup/`).

- Script yang digunakan: `backup.sh`.
- Direktori sumber: `/srv/fileserver/share`.
- Direktori tujuan: `/srv/fileserver/backup`.
- Format arsip: `.tar.gz`.
- Tujuan: Membuat salinan data dari direktori bersama agar dapat digunakan kembali apabila terjadi kehilangan atau kerusakan data.
- Hasil yang dituju: Menghasilkan arsip backup dengan nama berdasarkan waktu pembuatan.

### B. Implementasi Verifikasi Checksum SHA-256

Menerapkan pemeriksaan integritas arsip backup menggunakan algoritma SHA-256.

- Perintah yang digunakan: `sha256sum` dan `sha256sum -c`.
- File yang diperiksa: Arsip backup `.tar.gz`.
- Tujuan: Memastikan arsip backup tidak mengalami perubahan atau kerusakan sebelum dilakukan proses restore.
- Hasil yang dituju: Arsip yang memiliki checksum sesuai dinyatakan valid, sedangkan arsip yang mengalami perubahan akan ditolak.

### C. Implementasi Restore

Mengerjakan proses pemulihan data dari arsip backup ke direktori pengujian.

- Script yang digunakan: `restore.sh`.
- Direktori tujuan pemulihan: `/srv/fileserver/restore-test`.
- Tujuan: Mengembalikan data dari arsip backup tanpa langsung mengubah data asli pada direktori share.
- Pengujian: Membandingkan hasil pemulihan dengan data sumber menggunakan perintah `diff -r`.

### D. Implementasi Sinkronisasi Menggunakan flock

Menerapkan mekanisme penguncian (locking) untuk mencegah terjadinya dua proses backup atau restore yang berjalan bersamaan.

- Perintah yang digunakan: `flock`.
- Opsi yang digunakan: `flock -n -E 75`.
- Tujuan: Mencegah konflik ketika dua proses mencoba mengakses atau menulis arsip backup secara bersamaan.
- Hasil yang dituju: Proses pertama dapat berjalan, sedangkan proses kedua ditolak dengan exit status 75 apabila lock sedang digunakan.

### E. Pengujian dan Analisis Hasil

Melakukan pengujian untuk memastikan seluruh mekanisme backup, restore, checksum, dan locking berjalan sesuai rancangan.

- Pengujian positif: Membuat arsip backup dan melakukan verifikasi checksum.
- Pengujian positif: Melakukan restore dan membandingkan hasilnya dengan data sumber.
- Pengujian negatif: Mengubah satu byte pada arsip backup untuk memastikan checksum mendeteksi perubahan.
- Pengujian sinkronisasi: Menjalankan dua proses backup secara bersamaan untuk memastikan proses kedua ditolak ketika lock sedang digunakan.

## 4. Skenario Pengujian

| Jenis Pengujian | Skenario | Hasil Aktual |
|---|---|---|
| Positif (+) | Menjalankan proses backup menggunakan script `backup.sh`. | [Isi sesuai hasil pengujian aktual] |
| Positif (+) | Memeriksa integritas arsip menggunakan `sha256sum -c`. | [Isi sesuai hasil pengujian aktual] |
| Positif (+) | Melakukan restore menggunakan script `restore.sh`. | [Isi sesuai hasil pengujian aktual] |
| Positif (+) | Membandingkan direktori sumber dan hasil restore menggunakan `diff -r`. | [Isi sesuai hasil pengujian aktual] |
| Negatif (-) | Mengubah satu byte pada arsip backup untuk menguji kerusakan data. | [Isi sesuai hasil pengujian aktual] |
| Negatif (-) | Melakukan restore terhadap arsip yang checksum-nya tidak sesuai. | [Isi sesuai hasil pengujian aktual] |
| Negatif (-) | Menjalankan dua proses backup secara bersamaan. | [Isi sesuai hasil pengujian aktual] |

## 5. Bukti Pekerjaan

### 1. Implementasi Backup

![Proses Backup](evidence/backup.jpg)

Menampilkan proses pencadangan data dari direktori share ke direktori backup menggunakan script `backup.sh`. Proses ini menghasilkan arsip dengan format `.tar.gz` berdasarkan waktu pembuatan.

### 2. Pemeriksaan Arsip Backup

![Hasil Arsip Backup](evidence/arsip-backup.jpg)

Menampilkan hasil arsip backup yang berhasil dibuat pada direktori `/srv/fileserver/backup`.

### 3. Verifikasi Checksum SHA-256

![Verifikasi Checksum](evidence/checksum.jpg)

Menampilkan proses pemeriksaan integritas arsip menggunakan perintah `sha256sum -c` untuk memastikan arsip backup tidak mengalami perubahan atau kerusakan.

### 4. Pengujian Restore

![Pengujian Restore](evidence/restore.jpg)

Menampilkan proses pemulihan data dari arsip backup ke direktori `restore-test` menggunakan script `restore.sh`.

### 5. Perbandingan Hasil Restore

![Perbandingan Data](evidence/diff-restore.jpg)

Menampilkan hasil perbandingan antara direktori sumber dan direktori hasil restore menggunakan perintah `diff -r` untuk memastikan data hasil pemulihan sesuai dengan data asli.

### 6. Pengujian Negatif: Arsip Backup Rusak

![Pengujian Arsip Rusak](evidence/backup-rusak.jpg)

Menampilkan pengujian dengan mengubah salah satu byte pada arsip backup untuk memastikan sistem dapat mendeteksi ketidaksesuaian checksum dan menolak proses restore.

### 7. Pengujian Sinkronisasi flock

![Pengujian flock](evidence/flock.jpg)

Menampilkan pengujian dua proses backup yang dijalankan secara bersamaan. Proses kedua seharusnya ditolak dengan exit status 75 ketika proses pertama masih memegang lock.

## 6. Informasi GitHub

| Keterangan | Isi |
|---|---|
| Repository kelompok | https://github.com/kel2-so/fileserver-6a |
| Repository fork pribadi | https://github.com/khls07/fileserver-6a |
| Commit hash pekerjaan | [Isi commit hash] |
| Pesan commit | Implementasi Backup, Restore, Verifikasi SHA-256, dan Locking flock |
| Status PORTOFOLIO.md | Sudah dibuat |

## 7. Kendala dan Penyelesaian

**Kendala yang ditemukan:**

Kendala dalam pengerjaan bagian backup dan restore adalah memastikan arsip yang dihasilkan benar-benar utuh dan dapat digunakan untuk memulihkan data. Selain itu, proses backup yang berjalan secara bersamaan berpotensi menyebabkan konflik penulisan arsip, seperti penggunaan nama file yang sama atau ketidaksesuaian antara arsip dan file checksum.

**Langkah penyelesaian:**

Menerapkan proses backup menggunakan perintah `tar` untuk membuat arsip dengan format `.tar.gz`. Arsip terlebih dahulu ditulis menggunakan nama sementara dengan ekstensi `.tmp`, kemudian diubah menjadi nama arsip final setelah proses berhasil. Selanjutnya, menggunakan `sha256sum` untuk menghasilkan checksum dan `sha256sum -c` untuk memverifikasi integritas arsip sebelum restore dilakukan.

Untuk mencegah konflik proses, diterapkan mekanisme penguncian menggunakan `flock -n -E 75`. Dengan mekanisme tersebut, proses backup atau restore yang sedang berjalan akan memegang lock, sedangkan proses lain yang mencoba menggunakan lock yang sama akan ditolak. Setelah proses restore selesai, hasil pemulihan diperiksa menggunakan `diff -r` untuk memastikan kesesuaiannya dengan data sumber.

## 8. Kesimpulan

Melalui bagian pekerjaan Backup dan Restore, saya mempelajari penerapan sistem pencadangan dan pemulihan data pada sistem operasi Linux. Saya memahami penggunaan perintah `tar` untuk membuat arsip, `sha256sum` untuk memeriksa integritas data, serta `flock` untuk menerapkan mekanisme sinkronisasi agar tidak terjadi konflik ketika beberapa proses dijalankan secara bersamaan.

Pengujian backup, restore, verifikasi checksum, dan locking menjadi bagian penting untuk memastikan data dapat dicadangkan dan dipulihkan dengan aman. Dengan demikian, implementasi yang dikerjakan membantu menjaga integritas dan ketersediaan data pada sistem Server Berkas Bersama.

---

**Nama:** Muhammad Ikhlas Aulya

**NIM:** 2510512198

**Tanggal pembaruan:** 15 November 2026
