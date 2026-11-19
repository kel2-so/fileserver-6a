# PORTOFOLIO.md

## Identitas
- Nama: Fricelmo Rikar Weohawu Thalo
- NIM: 2510512192
- Kelas/Kelompok: Kelas E, Kelompok 02
- Proyek: 6A Server Berkas Bersama (Samba) dan Audit Akses

## Asal proyek
Proyek ini dikerjakan berkelompok, bukan karya pribadi.
- Repository utama: https://github.com/kel2-so/fileserver-6a
- Anggota: Mario Dionisius Pake, Zahara Marchela, Fricelmo Rikar Weohawu Thalo, Salma Kamila Arifin, Muhammad Ikhlas Aulya, Anisa Nugrahini, Dimas Dwi Surya

## Kontribusi pribadi
Peran: Samba Client (anggota 3), yaitu menguji akses ke share Samba dari komputer Windows ke server Ubuntu.
- Menguji konektivitas SMB (port 445).
- Menguji akses akun berwenang dan penolakan pada kondisi negatif.
- Menyusun dokumen hasil uji beserta bukti.

## Bukti kontribusi
- Commit: https://github.com/kel2-so/fileserver-6a/commit/1035d48
- Pull Request: https://github.com/kel2-so/fileserver-6a/pull/1
- Berkas: tests/t2_samba_windows.md dan 3 screenshot di evidence/

## Skenario individu
Lingkungan: Windows 11 (klien 192.168.1.39) ke Ubuntu (server 192.168.1.48), share `berkas`, akun `op1`. Tanggal uji: 11/11/2026.

| ID | Kondisi | Perintah | Hasil |
|----|---------|----------|-------|
| T3-P0 | Positif | Test-NetConnection 192.168.1.48 -Port 445 | TcpTestSucceeded : True |
| T3-P1 | Positif | net use \\192.168.1.48\berkas /user:op1, lalu start | Perintah sukses; folder terbuka, 5 berkas terlihat |
| T3-N1 | Negatif | net use ... /user:op1 (password salah) | System error 86 |
| T3-N2 | Negatif | start \\192.168.1.48\berkas tanpa kredensial valid | Access is denied |

Pemulihan: net use * /delete

Keterbatasan: exit status (%errorlevel%) belum tercatat; pembuatan berkas dari Windows belum didokumentasikan; akun Samba yang ada tetapi tidak berwenang belum diuji; dugaan penyebab pesan SMB signing belum diverifikasi lewat log Samba.

## Analisis konsep SO
- **Autentikasi vs otorisasi:** error 86 (password salah) terjadi di tahap autentikasi, sedangkan "Access is denied" tanpa kredensial valid adalah penolakan akses. Keduanya berbeda penyebab.
- **Proteksi berkas:** akses lewat Samba harus lolos aturan Samba dan permission pada sistem berkas Linux di server.
- **Komunikasi jaringan dan I/O:** klien mengakses berkas lewat protokol SMB di port 445, sehingga hasil uji bergantung pada konektivitas, autentikasi, dan kebijakan keamanan klien.
aku j
## Kendala dan penyelesaian
- Pesan "SMB signing" saat membuka share tanpa akun. Diselesaikan dengan menghubungkan lebih dulu memakai `net use` dengan akun `op1`. Penyebabnya masih dugaan.
- Git: `Authentication failed` dan `Repository not found` karena login akun yang salah; diselesaikan dengan menghapus kredensial lama dan login sebagai Fricelmo.
- Git: `nothing to commit` karena berkas bukti belum disalin ke folder repository; diselesaikan dengan menyalin berkas lalu `git add`.
- Terminal Git Bash macet setelah menjalankan `notepad`; diselesaikan dengan menutup terminal dan membuat berkas lewat Windows.

## Refleksi
Sebelumnya saya mengira Git tidak sekompleks ini. Ternyata satu pekerjaan kecil, yaitu mengirim bukti uji, melewati banyak tahap: clone, branch, add, commit, push, pull request, lalu merge. Saya juga sempat salah akun GitHub, salah login di Git Bash, dan berkas yang belum disalin ke folder repository, sehingga muncul pesan seperti "Authentication failed" dan "nothing to commit". Dari situ saya paham bahwa Git punya aturan yang ketat tentang siapa yang mengirim dan apa yang dikirim.

Yang sudah saya kuasai: menguji akses Samba dari Windows ke Ubuntu, membedakan error autentikasi (system error 86) dari penolakan akses ("Access is denied"), serta alur kerja Git lewat branch dan pull request sampai hasil kerja saya masuk ke repository kelompok.

Yang masih perlu saya pelajari: membaca log Samba di server untuk memastikan penyebab pesan SMB signing, menguji akun yang ada di Samba tetapi tidak berwenang, mencatat exit status (%errorlevel%) pada setiap pengujian, dan memahami permission serta ACL di sisi server Linux, bukan hanya dari sisi klien.

## Sumber pihak lain
Draf struktur repository dan templat dokumen dibantu oleh Claude (Anthropic); isi hasil uji berasal dari pengujian sendiri.
