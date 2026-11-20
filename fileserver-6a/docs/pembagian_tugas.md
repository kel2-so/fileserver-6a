## Pembagian Tugas Proyek 6A (Kelompok 2) — 7 Anggota

| Anggota |Nama/NIM| Tanggung Jawab | Testing Positif | Testing Negatif | Kode / File yang Dikerjakan |
|---|---|---|---|---|---|
| 1 | Mario Dionisius Pake/2510512201 | User, Group, Permission | Operator dapat membuat dan menulis file | Pengguna di luar grup ditolak | `setup.sh`, `t1_permission.sh` |
| 2 | Zahara Marchela/2510512200 | Samba Server | Samba aktif, konfigurasi valid, dan share tersedia | Akun tidak berwenang ditolak server | `config/smb_share.conf`, konfigurasi Samba, `t2_samba.sh` |
| 3 | Fricelmo Rikar Weohawu Thalo/2510512192 | Samba Client | Klien berhasil terhubung dan mengakses share sesuai haknya | Klien tidak berwenang gagal mengakses share | Pengujian client `smbclient`, pengujian akses share |
| 4 | Salma Kamila Arifin/2510512191 | Hak Pembaca (Reader) | Reader dapat membaca dan mengunduh file | Reader tidak dapat mengubah atau menghapus file | ACL di `setup.sh`, `t3_reader.sh` |
| 5 | Muhammad Ikhlas Aulya/2510512198 | Administrasi SSH | Admin berhasil login dan menjalankan perintah administrasi yang diizinkan | Akun biasa ditolak untuk tindakan admin | `ssh_fileserver.conf`, `sudoers_admin.example`, `t4_ssh_admin.sh` |
| 6 | Anisa Nugrahini/2510512182 | Backup dan Restore | Backup berhasil dibuat dan data berhasil dipulihkan | Backup rusak atau checksum tidak valid ditolak | `backup.sh`, `restore.sh`, `t5_backup_restore.sh` |
| 7 | Dimas Dwi Surya/2510512196 | Monitoring, Log, Laporan, Docker | Monitoring berjalan, laporan terbentuk, dan Docker dapat membaca laporan | Layanan berhenti terdeteksi, Docker gagal menulis melalui mount read-only | `check_services.sh`, `monitor.sh`, `gen_report.sh`, `t6_monitor_report.sh`, `docker_report.sh`, `t7_docker.sh`, `run_all.sh`, `cleanup.sh` |

### Ketentuan Kontribusi

Setiap anggota wajib mengerjakan bagian sesuai tanggung jawabnya, melakukan pengujian positif dan negatif, menuliskan analisis hasil pengujian pada laporan, serta membuat commit GitHub atas kontribusinya masing-masing.
