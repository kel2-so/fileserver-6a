
# PORTOFOLIO KONTRIBUSI PROYEK SISTEM OPERASI

**Topik:** Server Berkas Bersama (Samba) & Audit Akses

## 1. Identitas Mahasiswa

| Keterangan | Isi |
|---|---|
| Nama | Salma Kamila Arifin |
| NIM | 2510512191 |
| Kelas / Kelompok | E/Kelompok 2 |
| Mata Kuliah | Sistem Operasi |
| Tanggung Jawab | Hak Akses Reader (Permission dan ACL) |
| Repository Kelompok | https://github.com/kel2-so/fileserver-6a |

## 2. Deskripsi Tanggung Jawab

Saya bertanggung jawab pada bagian Hak Akses Reader (Analisis Permission dan Access Control List/ACL) dalam proyek Server Berkas Bersama. Fokus pekerjaan saya adalah menganalisis dan mengatur hak akses pengguna dengan role reader pada direktori bersama, serta melakukan pengujian untuk memastikan bahwa pengguna reader hanya dapat membaca dokumen tanpa memiliki izin untuk membuat maupun menghapus file.

## 3. Rincian Pekerjaan

### A. Analisis Permission Linux

Menganalisis penggunaan permission Linux untuk mengatur hak akses terhadap direktori dan file pada server berkas bersama.

- Jenis permission yang dianalisis: read (r), write (w), dan execute (x).
- Tujuan: Memastikan pengguna reader memperoleh izin sesuai dengan perannya.
- Hasil analisis: Pengguna reader diberikan akses membaca tanpa izin untuk mengubah atau menghapus file.

### B. Analisis Access Control List (ACL)

Menganalisis penggunaan ACL untuk memberikan hak akses secara lebih spesifik kepada pengguna atau grup reader.

- Perintah yang digunakan: `getfacl` dan `setfacl`.
- Lokasi direktori yang diperiksa: `/srv/fileserver/share` [Sesuaikan dengan konfigurasi aktual].
- Hak akses yang dituju: Reader dapat membaca dokumen, tetapi tidak dapat membuat maupun menghapus file.

### C. Pengujian Hak Akses Reader

Melakukan pengujian menggunakan akun reader untuk memastikan hak akses berjalan sesuai konfigurasi.

- User reader: `rd1`.
- Direktori pengujian: `/srv/fileserver/share`
- Pengujian positif: Membaca dokumen.
- Pengujian negatif: Membuat file baru, mengubah nama file (rename), mengedit isi file, menghapus file.

### D. Analisis Hasil Pengujian

Menganalisis hasil pengujian untuk memastikan pembatasan hak akses reader berjalan sesuai tujuan.

- Hasil yang diharapkan: Reader berhasil membaca dokumen yang tersedia di direktori bersama.
- Hasil yang diharapkan: Reader ditolak saat mencoba membuat file baru.
- Hasil yang diharapkan: Reader ditolak saat mencoba mengubah nama (rename) file.
- Hasil yang diharapkan: Reader ditolak saat mencoba mengedit isi file.
- Hasil yang diharapkan: Reader ditolak saat mencoba menghapus file.

## 4. Skenario Pengujian

| Jenis Pengujian | Skenario | Hasil Aktual |
|---|---|---|
| Positif (+) | Reader membaca dokumen pada direktori bersama. | Berhasil membaca dokumen menggunakan akun rd1. |
| Negatif (-) | Reader membuat file baru. | Gagal membuat file karena tidak memiliki izin tulis (write). |
| Negatif (-) | Reader mengubah nama file (rename). | Gagal mengubah nama file karena tidak memiliki izin tulis pada direktori. |
| Negatif (-) | Reader mengedit isi file. | Gagal menyimpan perubahan karena tidak memiliki izin tulis. |
| Negatif (-) | Reader menghapus file. | Gagal menghapus file karena tidak memiliki izin tulis pada direktori. |

## 5. Bukti Pekerjaan

### 1. Pemeriksaan Permission Direktori

permission

![Pemeriksaan Permission](evidence/permission.jpg)

Menampilkan hasil pemeriksaan hak akses direktori bersama menggunakan perintah `ls -ld`.

### 2. Pemeriksaan Access Control List (ACL)

![Pemeriksaan ACL](evidence/acl.jpg)

Menampilkan pengaturan hak akses pengguna dan grup pada direktori bersama menggunakan perintah `getfacl`.

### Lalu masuk ke pengujian

![Menghapus Koneksi Samba](evidence/menghapus%20koneksi%20samba.jpg)

Menghapus koneksi Samba sebelumnya agar dapat melakukan autentikasi ulang menggunakan akun yang akan diuji.

![Autentikasi OP1](evidence/op1%20autentikasi.jpg)

Pengguna op1 berhasil melakukan autentikasi ke shared folder Samba.

![Windows Client](evidence/windows%20client.jpg)

Shared folder berhasil dibuka dari komputer client Windows.

### 3. Pengujian Positif: Membaca Dokumen

![Pengujian Membaca Dokumen](evidence/read.jpg)

### 4. Pengujian Negatif: Membuat File

![Pengujian Membuat File](evidence/create.jpg)

### 5. Pengujian Negatif: Menghapus File

![Pengujian Menghapus File](evidence/delete.jpg)

### 6. Pengujian Negatif: Mengedit nama File

![Pengujian Rename File](evidence/rename.jpg)

## 6. Informasi GitHub

| Keterangan | Isi |
|---|---|
| Repository kelompok | https://github.com/kel2-so/fileserver-6a |
| Repository fork pribadi | https://github.com/kamila-sall/fileserver-6a |
| Commit hash pekerjaan | 70be4b1 |
| Pesan commit | Pengujian Hak Akses Reader menggunakan Permission dan ACL |
| Status PORTOFOLIO.md | Sudah dibuat |

## 7. Kendala dan Penyelesaian

**Kendala yang ditemukan:**

Kendala yang ditemukan adalah memastikan bahwa pengguna dengan hak akses reader hanya dapat membaca dokumen tanpa memiliki izin untuk mengubah isi file, membuat file baru, mengganti nama file, maupun menghapus file. Selain itu, diperlukan pemeriksaan konfigurasi permission dan Access Control List (ACL) untuk memastikan hak akses yang diberikan sudah sesuai.

**Langkah penyelesaian:**

Melakukan pemeriksaan keanggotaan pengguna rd1 pada grup sf_reader menggunakan perintah `id rd1`. Selanjutnya, memeriksa hak akses direktori menggunakan perintah `ls -ld` dan `getfacl` untuk memastikan grup reader hanya memiliki izin baca dan akses direktori (r-x). Setelah itu, melakukan pengujian melalui laptop client dengan mengakses folder Samba menggunakan akun reader untuk memastikan pengguna dapat membaca dokumen, tetapi tidak dapat membuat, mengubah, mengganti nama, atau menghapus file.

## 8. Kesimpulan

Melalui bagian pekerjaan Hak Akses Reader, saya mempelajari penggunaan permission Linux dan Access Control List (ACL) untuk mengatur serta membatasi hak akses pengguna pada direktori bersama. Pengujian dilakukan untuk memastikan bahwa pengguna dengan hak akses reader dapat membaca dokumen, tetapi tidak dapat membuat, mengubah isi, mengganti nama, maupun menghapus file. Dengan demikian, pengaturan hak akses yang sesuai dapat membantu menjaga keamanan dan integritas dokumen pada server berkas bersama.

---

**Nama:** Salma Kamila Arifin

**NIM:** 2510512191

**Tanggal pembaruan:** 15 November 2026