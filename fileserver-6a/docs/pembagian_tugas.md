## Pembagian Tugas Proyek 6A (Kelompok 2) — 7 Anggota

| Anggota |Nama/NIM| Tanggung Jawab | Testing Positif | Testing Negatif | Kode / File yang Dikerjakan |
|---|---|---|---|---|---|
| 1 | Mario Dionisius Pake/2510512201 | User, Group, Permission | Operator dapat membuat dan menulis file | Pengguna di luar grup ditolak | `scripts/setup.sh`, `tests/t1_permission.sh` |
| 2 | Zahara Marchela/2510512200 | Samba Server | Samba aktif, konfigurasi valid, dan share tersedia | Akun tidak berwenang ditolak server | `config/smb_share.conf`, bagian konfigurasi server pada `tests/t2_samba.sh` |
| 3 | Fricelmo Rikar Weohawu Thalo/2510512192 | Samba Client | Klien berhasil terhubung dan mengakses share sesuai haknya | Klien tidak berwenang gagal mengakses share | Bagian pengujian client pada `tests/t2_samba.sh` |
| 4 | Salma Kamila Arifin/2510512191 | Hak Pembaca (Reader) | Reader dapat membaca dan mengunduh file | Reader tidak dapat mengubah atau menghapus file | Bagian konfigurasi ACL pada `scripts/setup.sh`, `tests/t3_reader.sh` |
| 5 | Muhammad Ikhlas Aulya/2510512198 | Administrasi SSH | Admin berhasil login dan menjalankan perintah administrasi yang diizinkan | Akun biasa ditolak untuk tindakan admin | `config/sshd_fileserver.conf`, `config/sudoers_sfadmin.example`, `tests/t4_ssh_admin.sh` |
| 6 | Anisa Nugrahini/2510512182 | Backup dan Restore | Backup berhasil dibuat dan data berhasil dipulihkan | Backup rusak atau checksum tidak valid ditolak | `scripts/backup.sh`, `scripts/restore.sh`, `tests/t5_backup_restore.sh` |
| 7 | Dimas Dwi Surya/2510512196 | Monitoring, Log, Laporan, Docker | Monitoring berjalan, laporan terbentuk, dan Docker dapat membaca laporan | Layanan berhenti terdeteksi, Docker gagal menulis melalui mount read-only | `scripts/check_services.sh`, `scripts/monitor.sh`, `scripts/gen_report.sh`, `scripts/docker_report.sh`, `tests/t6_monitor_report.sh`, `tests/t7_docker.sh`, `tests/run_all.sh`, `scripts/cleanup.sh` |

## Catatan Pembagian Tugas

1. File `scripts/setup.sh` digunakan bersama oleh Anggota 1 dan Anggota 4. Anggota 1 berfokus pada user, group, dan permission, sedangkan Anggota 4 berfokus pada konfigurasi ACL untuk hak akses Reader.
2. Pengujian Samba Server dan Samba Client berada dalam satu file, yaitu `tests/t2_samba.sh`. Anggota 2 bertanggung jawab pada sisi server, sedangkan Anggota 3 berfokus pada pengujian dari sisi client.
3. File implementasi disimpan dalam folder `scripts/`, file konfigurasi dalam folder `config/`, dan file pengujian dalam folder `tests/`.
4. Seluruh pengujian proyek dapat dijalankan melalui `tests/run_all.sh`.

## Ketentuan Kontribusi

Setiap anggota wajib:
1. Mengerjakan bagian proyek sesuai tanggung jawab yang telah ditentukan.
2. Melakukan pengujian positif dan negatif pada fitur yang dikerjakan.
3. Menuliskan hasil dan analisis pengujian pada laporan.
4. Membuat commit dan push ke GitHub sebagai bukti kontribusi masing-masing.
5. Berkoordinasi dengan anggota lain apabila terdapat file atau fitur yang dikerjakan bersama.
