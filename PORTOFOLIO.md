# PORTOFOLIO KONTRIBUSI PROYEK SISTEM OPERASI

**Topik:** Server Berkas Bersama (Samba) & Audit Akses

## 1. Identitas Mahasiswa

| Keterangan | Isi |
|---|---|
| Nama | Muhammad Ikhlas Aulya |
| NIM | 2510512198 |
| Kelas / Kelompok | E/Kelompok 2 |
| Mata Kuliah | Sistem Operasi |
| Tanggung Jawab | Administrasi SSH (Keamanan Akses Jarak Jauh dan Hak Administrator) |
| Repository Kelompok | https://github.com/kel2-so/fileserver-6a |

## 2. Deskripsi Tanggung Jawab

Saya bertanggung jawab pada bagian Administrasi SSH (Secure Shell) dalam proyek Server Berkas Bersama. Fokus pekerjaan saya adalah mengatur dan menganalisis keamanan akses jarak jauh pada server Linux, serta melakukan pembatasan akses pengguna agar hanya administrator atau pengguna yang termasuk grup yang diizinkan dapat melakukan koneksi SSH. Pengujian dilakukan untuk memastikan pengguna yang memiliki izin dapat masuk ke server, sedangkan pengguna yang tidak memiliki izin akan ditolak.

## 3. Rincian Pekerjaan

### A. Analisis Secure Shell (SSH)

Menganalisis penggunaan SSH sebagai layanan untuk mengakses dan mengelola server Linux dari jarak jauh secara aman.

- Fungsi SSH: Memungkinkan administrator melakukan akses jarak jauh ke server melalui jaringan.
- Tujuan: Memudahkan administrasi server tanpa harus mengakses komputer server secara langsung.
- Hasil analisis: SSH membantu proses pengelolaan server dengan menyediakan koneksi jarak jauh yang aman.

### B. Konfigurasi dan Pembatasan Akses SSH

Menganalisis dan melakukan pengaturan layanan SSH agar akses ke server hanya diberikan kepada pengguna yang diizinkan.

- Layanan yang digunakan: `ssh` atau `sshd`.
- File konfigurasi: `/etc/ssh/sshd_config`.
- Fokus konfigurasi: Pembatasan pengguna atau grup yang diperbolehkan melakukan koneksi SSH.
- Tujuan: Mencegah pengguna yang tidak memiliki izin mengakses server melalui SSH.
- Catatan: Pengaturan pengguna atau grup disesuaikan dengan konfigurasi aktual pada server.

### C. Pengujian Koneksi SSH

Melakukan pengujian menggunakan akun administrator dan akun pengguna yang tidak termasuk dalam grup yang diizinkan.

- Layanan pengujian: SSH.
- Pengujian positif: Administrator berhasil melakukan koneksi SSH ke server.
- Pengujian negatif: Pengguna yang tidak termasuk grup yang diizinkan ditolak saat melakukan koneksi SSH.
- Tujuan: Memastikan pembatasan akses SSH berjalan sesuai aturan keamanan.

### D. Analisis Hasil Pengujian

Menganalisis hasil pengujian untuk memastikan layanan SSH dan pembatasan akses pengguna berjalan sesuai tujuan.

- Hasil yang diharapkan: Administrator berhasil melakukan koneksi SSH.
- Hasil yang diharapkan: Pengguna yang termasuk grup yang diizinkan dapat mengakses server.
- Hasil yang diharapkan: Pengguna di luar grup yang diizinkan ditolak saat mencoba melakukan koneksi SSH.
- Hasil analisis: Pembatasan akses SSH membantu menjaga keamanan server dari akses jarak jauh yang tidak sah.

## 4. Skenario Pengujian

| Jenis Pengujian | Skenario | Hasil Aktual |
|---|---|---|
| Positif (+) | Administrator melakukan koneksi SSH ke server. | [Isi sesuai hasil pengujian sebenarnya] |
| Negatif (-) | Pengguna yang tidak termasuk grup yang diizinkan mencoba melakukan koneksi SSH. | [Isi sesuai hasil pengujian sebenarnya] |

## 5. Bukti Pekerjaan

### 1. Pemeriksaan Status Layanan SSH

![Pemeriksaan Status SSH](evidence/status-ssh.jpg)

Menampilkan hasil pemeriksaan status layanan SSH untuk memastikan layanan berjalan pada server Linux.

### 2. Pemeriksaan Konfigurasi SSH

![Konfigurasi SSH](evidence/konfigurasi-ssh.jpg)

Menampilkan konfigurasi SSH yang digunakan untuk mengatur pembatasan akses pengguna atau grup yang diizinkan.

### 3. Pengujian Positif: Koneksi Administrator

![Pengujian SSH Administrator](evidence/ssh-berhasil.jpg)

Menampilkan hasil pengujian ketika administrator berhasil melakukan koneksi SSH ke server.

### 4. Pengujian Negatif: Koneksi Pengguna Tidak Diizinkan

![Pengujian SSH Ditolak](evidence/ssh-ditolak.jpg)

Menampilkan hasil pengujian ketika pengguna yang tidak termasuk grup yang diizinkan ditolak saat mencoba melakukan koneksi SSH.

## 6. Informasi GitHub

| Keterangan | Isi |
|---|---|
| Repository kelompok | https://github.com/kel2-so/fileserver-6a |
| Repository fork pribadi | https://github.com/khls07/fileserver-6a |
| Commit hash pekerjaan | 05c52e3 |
| Pesan commit | Konfigurasi dan Pengujian Administrasi SSH |
| Status PORTOFOLIO.md | Sudah dibuat setelah file berhasil ditambahkan ke repository |

## 7. Kendala dan Penyelesaian

**Kendala yang ditemukan:**

Kendala yang perlu diperhatikan dalam administrasi SSH adalah memastikan bahwa hanya administrator atau pengguna yang termasuk grup yang diizinkan dapat melakukan koneksi jarak jauh ke server. Selain itu, konfigurasi layanan SSH harus diperiksa agar pembatasan akses berjalan sesuai aturan yang telah ditentukan.

**Langkah penyelesaian:**

Melakukan pemeriksaan status layanan SSH untuk memastikan layanan berjalan dengan baik. Selanjutnya, memeriksa konfigurasi SSH pada file `/etc/ssh/sshd_config` untuk memastikan aturan pembatasan pengguna atau grup sudah sesuai. Setelah itu, melakukan pengujian koneksi menggunakan akun administrator dan akun pengguna yang tidak diizinkan untuk memastikan akses diberikan atau ditolak sesuai aturan.

## 8. Kesimpulan

Melalui bagian pekerjaan Administrasi SSH, saya mempelajari penggunaan Secure Shell (SSH) untuk melakukan administrasi server Linux dari jarak jauh. Saya juga memahami pentingnya keamanan akses jarak jauh dan pembatasan hak akses administrator agar server tidak dapat diakses oleh pengguna yang tidak memiliki izin. Pengujian dilakukan untuk memastikan administrator yang diizinkan berhasil melakukan koneksi SSH, sedangkan pengguna di luar grup yang diizinkan ditolak. Dengan demikian, pengaturan SSH yang tepat dapat membantu meningkatkan keamanan server berkas bersama.

---

**Nama:** Muhammad Ikhlas Aulya

**NIM:** 2510512198

**Tanggal pembaruan:** 15 November 2026
