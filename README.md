# Server Berkas Bersama dengan Backup dan Audit Akses (6A)

![Ubuntu](https://img.shields.io/badge/Ubuntu_Server-25.04-E95420?logo=ubuntu&logoColor=white)
![Samba](https://img.shields.io/badge/Samba-4.23.6-blue)
![OpenSSH](https://img.shields.io/badge/OpenSSH-10.2p1-black?logo=openssh&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-29.1.3-2496ED?logo=docker&logoColor=white)

**Proyek Akhir Sistem Operasi (Kelompok 2)**

## Anggota Kelompok

| No. | Nama | NIM |
|---|---|---|
| 1 | Anisa Nugrahini | 2510512182 |
| 2 | Dimas Dwi Surya | 2510512196 |
| 3 | Fricelmo Rikar Weohawu Thalo | 2510512192 |
| 4 | Mario Dionisius Pake | 2510512201 |
| 5 | Muhammad Ikhlas Aulya | 2510512198 |
| 6 | Salma Kamila Arifin | 2510512191 |
| 7 | Zahara Marchela | 2510512200 |

## Lingkungan Sistem

| Komponen | Versi |
|---|---|
| Sistem Operasi | Ubuntu Server 25.04 |
| Virtualisasi | Virtual Machine (VM) |
| Samba | 4.23.6-Ubuntu-4.23.6+dfsg-1ubuntu2.2 |
| OpenSSH | 10.2p1 Ubuntu-2ubuntu3.8 |
| Docker | 29.1.3 |
| Docker Image | Alpine 3.20 |

## Instalasi (urut, di VM)
1. `sudo apt update && sudo apt install -y samba acl openssh-server`
2. `git clone <repo> && cd proyek-6a`
3. `sudo scripts/setup_env.sh`  (grup, akun uji, direktori, permission/ACL, data dummy, pasang script ke /usr/local/sbin)
4. Atur kata sandi: `sudo passwd adm1` (juga op1, op2, tamu1) dan `sudo smbpasswd -a op1` (juga op2, rd1, rd2). Jangan daftarkan tamu1 ke Samba.
5. Tambahkan akun login Anda ke grup: `sudo usermod -aG sf_admin <akun-anda>`; buka satu sesi terminal cadangan.
6. `sudo scripts/setup_services.sh`  (blok Samba, sudoers terbatas, pembatasan SSH)

## Pengoperasian
- Backup: `sudo /usr/local/sbin/fs-backup.sh`
- Restore ke restore-test/: `sudo /usr/local/sbin/fs-restore.sh <nama-arsip>`
- Cek layanan: `sudo /usr/local/sbin/fs-check.sh` (atau `--loop 10`)
- Catat hasil uji akses: `sudo /usr/local/sbin/fs-logtest.sh T3-N "rd1 hapus ditolak" 1 LULUS`
- Laporan: `scripts/report.sh` (menulis output/laporan.txt)

## Docker (baca laporan, read-only)
    docker pull alpine:<tag>
    sha256sum output/laporan.txt > evidence/laporan.sha256.before
    docker run --rm --mount type=bind,src="$(pwd)/output",dst=/data,readonly alpine:<tag> cat /data/laporan.txt; echo "exit=$?"
    docker run --rm --mount type=bind,src="$(pwd)/output",dst=/data,readonly alpine:<tag> sh -c 'echo "uji perubahan" >> /data/laporan.txt'; echo "exit=$?"
    sha256sum -c evidence/laporan.sha256.before

## Pemulihan kondisi uji
`sudo scripts/cleanup.sh` (hapus hasil restore dan berkas uji; `--all` juga menghapus semua arsip dan log).

Uji lock: untuk G3 gunakan data dummy besar (~200 MB) agar backup berlangsung beberapa detik.
Langkah uji lengkap T1-T6 dan G1-G4: lihat laporan di docs/.
