# TESTING ANGGOTA 6 - BACKUP DAN RESTORE

**Nama:** Anisa Nugrahini  
**NIM:** 2510512182

---

## A. Testing Positif - Membuat Backup

**Output 1. Pemeriksaan isi direktori share sebelum backup**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo ls -l /srv/fileserver/share/

[sudo: authenticate] Password:             

total 36

-rwxrwx---+ 1 op1  op1          0 Nov  6 17:08 'New Text Document.txt'

-rwxrwx---+ 1 op1  op1         16 Nov  6 14:02  dokumen2.txt

-rwxrwx---+ 1 op1  op1         16 Nov  6 14:02  dokumen3.txt

-rwxrwx---+ 1 op1  op1         23 Nov  7 00:18  dokumen_1.txt

-rw-rw----+ 1 op1  sf_operator 29 Nov 18 13:22  t1.txt

-rw-rw----+ 1 root sf_operator 35 Nov 15 05:44  t2.txt

-rw-rw----+ 1 op1  sf_operator 18 Nov 18 13:39  t3.txt

-rw-rw----+ 1 op1  sf_operator  0 Nov 14 18:46  uji_operator.txt
```

**Output 2. Menjalankan script backup**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo /usr/local/sbin/fs-backup.sh

Backup selesai: backup_20261118_135712.tar.gz
```

**Output 3. Memeriksa file backup yang berhasil dibuat**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo ls -lh /srv/fileserver/backup/

total 611M

-rw-r----- 1 root root  283 Nov  6 20:15 backup_20261106_201541.tar.gz

-rw-r----- 1 root root   96 Nov  6 20:15 backup_20261106_201541.tar.gz.sha256

-rw-r----- 1 root root  279 Nov 14 18:21 backup_20261114_182153.tar.gz

-rw-r----- 1 root root   96 Nov 14 18:21 backup_20261114_182153.tar.gz.sha256

-rw-r----- 1 root root  279 Nov 14 18:24 backup_20261114_182439.tar.gz

-rw-r----- 1 root root   96 Nov 14 18:24 backup_20261114_182439.tar.gz.sha256

-rw-r----- 1 root root  334 Nov 14 18:58 backup_20261114_185858.tar.gz

-rw-r----- 1 root root   96 Nov 14 18:58 backup_20261114_185858.tar.gz.sha256

-rw-r----- 1 root root  334 Nov 14 18:59 backup_20261114_185934.tar.gz

-rw-r----- 1 root root   96 Nov 14 18:59 backup_20261114_185934.tar.gz.sha256

-rw-r----- 1 root root  334 Nov 14 19:01 backup_20261114_190110.tar.gz

-rw-r----- 1 root root   96 Nov 14 19:01 backup_20261114_190110.tar.gz.sha256

-rw-r----- 1 root root  11M Nov 14 19:04 backup_20261114_190445.tar.gz

-rw-r----- 1 root root   96 Nov 14 19:04 backup_20261114_190445.tar.gz.sha256

-rw-r----- 1 root root 201M Nov 14 19:06 backup_20261114_190604.tar.gz

-rw-r----- 1 root root   96 Nov 14 19:06 backup_20261114_190604.tar.gz.sha256

-rw-r----- 1 root root 201M Nov 18 13:53 backup_20261118_135307.tar.gz

-rw-r----- 1 root root   96 Nov 18 13:53 backup_20261118_135307.tar.gz.sha256

-rw-r----- 1 root root 201M Nov 18 13:57 backup_20261118_135712.tar.gz

-rw-r----- 1 root root   96 Nov 18 13:57 backup_20261118_135712.tar.gz.sha256

-rw-r----- 1 root root  100 Nov  6 21:18 backup_rusak.tar.gz

-rw-r--r-- 1 root root   86 Nov  6 21:22 backup_rusak.tar.gz.sha256
```

---

## B. Testing Positif - Memeriksa Integritas Backup

**Output 1. Memeriksa integritas backup menggunakan SHA256**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ cd /srv/fileserver/backup

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo sha256sum -c backup_20261118_135712.tar.gz.sha256

backup_20261118_135712.tar.gz: OK
```

---

## C. Testing Positif - Menguji Restore Data

**Output 1. Membuat data untuk pengujian restore**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ cd

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~$ cd ~/Downloads/proyek-6a

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo -u op1 bash -c 'echo "Data untuk pengujian restore" > /srv/fileserver/share/t1.txt'
```

**Output 2. Membuat backup setelah data pengujian ditambahkan**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo /usr/local/sbin/fs-backup.sh

Backup selesai: backup_20261118_140151.tar.gz
```

**Output 3. Menghapus file t1.txt dari direktori share**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo rm /srv/fileserver/share/t1.txt
```

**Output 4. Memeriksa isi direktori share setelah file dihapus**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo ls /srv/fileserver/share/

'New Text Document.txt'	  dokumen2.txt	 dokumen3.txt   dokumen_1.txt   t2.txt	 t3.txt	  uji_operator.txt
```

**Output 5. Menjalankan proses restore dari file backup**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo /usr/local/sbin/fs-restore.sh backup_20261118_140151.tar.gz

Restore selesai ke /srv/fileserver/restore-test/backup_20261118_140151 (berbeda dari share/ saat ini (share berubah setelah backup))
```

**Output 6. Memeriksa direktori hasil restore**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo ls -l /srv/fileserver/restore-test/

total 8

drwxrws--- 2 root sf_operator 4096 Nov  6 17:08 backup_20261106_201541

drwxrws--- 3 root sf_operator 4096 Nov 18 13:39 backup_20261118_140151
```

**Output 7. Mencari file t1.txt pada direktori hasil restore**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo find /srv/fileserver/restore-test/backup_20261118_140151 -name "t1.txt"

/srv/fileserver/restore-test/backup_20261118_140151/t1.txt
```

**Output 8. Memeriksa isi file t1.txt yang berhasil dipulihkan**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ sudo cat /srv/fileserver/restore-test/backup_20261118_140151/t1.txt

Data untuk pengujian restore
```

---

## D. Testing Negatif - Backup Rusak Ditolak

**Output 1. Menentukan nama file backup yang akan digunakan**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:~/Downloads/proyek-6a$ cd /srv/fileserver/backup

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ ARC="backup_261118_140151.tar.gz"
```

**Output 2. Mencoba menyalin file backup untuk pengujian**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo cp "$ARC" "${ARC%.tar.gz}_rusak.tar.gz"

cp: cannot stat 'backup_261118_140151.tar.gz': No such file or directory
```

**Output 3. Menentukan kembali nama file backup yang benar**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ cd /srv/fileserver/backup

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ ARC="backup_20261118_140151.tar.gz"
```

**Output 4. Menyalin file backup untuk membuat salinan pengujian**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo cp "$ARC" "${ARC%.tar.gz}_rusak.tar.gz"
```

**Output 5. Membuat file checksum untuk salinan backup**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo bash -c 'cd /srv/fileserver/backup && sed "s/$1/${1%.tar.gz}_rusak.tar.gz/" "$1.sha256" > "${1%.tar.gz}_rusak.tar.gz.sha256"' _ "$ARC"
```

**Output 6. Merusak isi file backup dengan menambahkan karakter X**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo bash -c 'printf X >> "$1"' _ "${ARC%.tar.gz}_rusak.tar.gz"
```

**Output 7. Menjalankan restore menggunakan file backup yang sudah rusak**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo /usr/local/sbin/fs-restore.sh "${ARC%.tar.gz}_rusak.tar.gz"

Verifikasi checksum GAGAL untuk backup_20261118_140151_rusak.tar.gz; restore dibatalkan
```

---

## E. Verifikasi Log Backup dan Restore

**Output 1. Memeriksa catatan aktivitas backup dan restore pada file log**

```bash
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:/srv/fileserver/backup$ sudo tail -n 20 /srv/fileserver/logs/ops.log

2026-11-06 21:22:25 mario-dionisius-pake ERROR Verifikasi checksum GAGAL untuk backup_rusak.tar.gz; restore dibatalkan

2026-11-06 21:50:52 mario-dionisius-pake OK smbd aktif PID=41557

2026-11-06 21:52:19 mario-dionisius-pake ERROR smbd tidak aktif

2026-11-06 21:53:29 mario-dionisius-pake OK smbd aktif PID=57699

2026-11-14 18:21:53 mario-dionisius-pake OK backup backup_20261114_182153.tar.gz ukuran=279

2026-11-14 18:24:39 mario-dionisius-pake OK backup backup_20261114_182439.tar.gz ukuran=279

2026-11-14 18:58:58 mario-dionisius-pake OK backup backup_20261114_185858.tar.gz ukuran=334

2026-11-14 18:59:34 mario-dionisius-pake OK backup backup_20261114_185934.tar.gz ukuran=334

2026-11-14 19:00:57 mario-dionisius-pake WARN lock dipegang proses lain

2026-11-14 19:01:10 mario-dionisius-pake OK backup backup_20261114_190110.tar.gz ukuran=334

2026-11-14 19:04:45 mario-dionisius-pake OK backup backup_20261114_190445.tar.gz ukuran=10488077

2026-11-14 19:06:12 mario-dionisius-pake OK backup backup_20261114_190604.tar.gz ukuran=209749845
```
