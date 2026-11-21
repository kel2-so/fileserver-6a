# Testing Monitoring Layanan, Pencatatan Akses, dan Integritas Laporan

**Penguji:** Anggota 7 - Dimas Dwi Surya
**Tanggal:** 21 November 2026
**Proyek:** fileserver-6a

## Tujuan

1. Memastikan skrip `fs-check.sh` dapat mendeteksi status layanan `smbd` (hidup, mati, dan pulih).
2. Memastikan hasil uji akses tercatat lewat `fs-logtest.sh`.
3. Memastikan laporan dapat dibuat lewat `scripts/report.sh`.
4. Membuktikan integritas `output/laporan.txt` (hash tidak berubah, dan file tidak bisa diubah dari container read-only).

---

## Langkah 1: Monitoring layanan dengan fs-check

### 1a. Kondisi smbd hidup

```bash
sudo /usr/local/sbin/fs-check.sh;  echo "exit=$?"
```

**Harapan:** `exit=0` (smbd hidup).

**Hasil:**

```
OK smbd aktif (PID 6294)
exit=0
```

**Status:** LULUS

### 1b. Kondisi smbd mati

```bash
sudo systemctl stop smbd
sleep 2
sudo /usr/local/sbin/fs-check.sh;  echo "exit=$?"
```

**Harapan:** `exit=1` (smbd mati).

**Hasil:**

```
ERROR smbd tidak aktif
exit=1
```

**Status:** LULUS

### 1c. Kondisi smbd pulih

```bash
sudo systemctl start smbd
sleep 3
sudo /usr/local/sbin/fs-check.sh;  echo "exit=$?"
```

**Harapan:** `exit=0` (smbd pulih).

**Hasil:**

```
OK smbd aktif (PID 7032)
exit=0
```

**Status:** LULUS (PID berubah dari 6294 ke 7032 karena smbd dijalankan ulang)

### 1d. Cek log operasional

```bash
sudo tail -n 20 "$LOG_DIR/ops.log"
```

**Hasil:**

```
2026-11-14 20:44:56 dimas OK smbd aktif PID=6788
2026-11-14 20:45:09 dimas ERROR smbd tidak aktif
2026-11-14 20:45:21 dimas OK smbd aktif PID=9329
2026-11-16 13:04:24 dimas OK backup backup_20261116_130424.tar.gz ukuran=246
2026-11-16 13:05:07 dimas OK smbd aktif PID=1791
2026-11-16 13:05:17 dimas OK smbd aktif PID=1791
2026-11-16 13:05:27 dimas ERROR smbd tidak aktif
2026-11-16 13:05:37 dimas ERROR smbd tidak aktif
2026-11-16 13:06:52 dimas OK smbd aktif PID=6246
2026-11-16 13:12:34 dimas OK smbd aktif PID=6246
2026-11-21 22:48:31 dimas OK smbd aktif PID=1611
2026-11-21 22:48:53 dimas ERROR smbd tidak aktif
2026-11-21 22:49:08 dimas OK smbd aktif PID=6294
2026-11-21 23:03:28 dimas OK smbd aktif PID=6294
2026-11-21 23:03:37 dimas ERROR smbd tidak aktif
2026-11-21 23:03:50 dimas OK smbd aktif PID=7032
```

**Catatan:** Setiap pemanggilan `fs-check.sh` tercatat di `ops.log`. Tiga baris terakhir (23:03:28, 23:03:37, 23:03:50) sesuai dengan urutan uji hidup, mati, dan pulih pada langkah 1a sampai 1c.

---

## Langkah 2: Pencatatan hasil uji akses

```bash
sudo /usr/local/sbin/fs-logtest.sh T3-N "Akses tamu ditolak" 1 LULUS
sudo cat "$LOG_DIR/access-tests.log"
```

**Harapan:** entri `T3-N` dengan keterangan "Akses tamu ditolak" dan status `LULUS` muncul di `access-tests.log`.

**Hasil:**

```
2026-11-14 20:52:04 T1-p | op1 berhasil membuat file | exit=0 | LULUS
2026-11-14 20:52:22 T4-N | rd1 gagal menghapus file | exit=1 | LULUS
2026-11-14 20:52:47 T3-N | tamu1 ditolak mengakses share | exit=2 | LULUS
2026-11-21 23:04:33 T3-N | Akses tamu ditolak | exit=1 | LULUS
```

**Status:** LULUS (entri baru tercatat pada baris terakhir)

---

## Langkah 3: Pembuatan laporan

Sebelum membuat laporan, backup dijalankan terlebih dahulu agar laporan memuat data backup terbaru.

```bash
sudo /usr/local/sbin/fs-backup.sh
sudo ls -l /srv/fileserver/backup/ | tail -n 6
```

**Hasil backup:**

```
Backup selesai: backup_20261121_230440.tar.gz
total 16
-rw-r----- 1 root root 246 Nov 16 13:04 backup_20261116_130424.tar.gz
-rw-r----- 1 root root  96 Nov 16 13:04 backup_20261116_130424.tar.gz.sha256
-rw-r----- 1 root root 247 Nov 21 23:04 backup_20261121_230440.tar.gz
-rw-r----- 1 root root  96 Nov 21 23:04 backup_20261121_230440.tar.gz.sha256
```

Pembuatan laporan:

```bash
ls scripts/
bash scripts/report.sh
cat output/laporan.txt
ls -l output/laporan.txt
```

**Harapan:** `report.sh` berjalan tanpa error dan `output/laporan.txt` terbentuk serta berisi laporan.

**Hasil:**

```
backup.sh  check_service.sh  cleanup.sh  log_test.sh  report.sh  restore.sh  setup_env.sh  setup_services.sh
Laporan ditulis: /home/dimas/PraktikumShell/proyek-6a/output/laporan.txt
LAPORAN SERVER BERKAS 6A
Dibuat : 2026-11-21 23:04:48

== Layanan smbd ==
Status : aktif (PID 7032)

== Backup terakhir ==
Arsip  : backup_20261121_230440.tar.gz
Waktu  : 2026-11-21 23:04:40
Ukuran : 247 byte
Verifikasi checksum : GAGAL atau berkas checksum tidak ada

== Hasil uji akses ==
2026-11-14 20:52:04 T1-p | op1 berhasil membuat file | exit=0 | LULUS
2026-11-14 20:52:22 T4-N | rd1 gagal menghapus file | exit=1 | LULUS
2026-11-14 20:52:47 T3-N | tamu1 ditolak mengakses share | exit=2 | LULUS
2026-11-21 23:04:33 T3-N | Akses tamu ditolak | exit=1 | LULUS

== 5 baris terakhir ops.log ==
2026-11-21 22:49:08 dimas OK smbd aktif PID=6294
2026-11-21 23:03:28 dimas OK smbd aktif PID=6294
2026-11-21 23:03:37 dimas ERROR smbd tidak aktif
2026-11-21 23:03:50 dimas OK smbd aktif PID=7032
2026-11-21 23:04:40 dimas OK backup backup_20261121_230440.tar.gz ukuran=247
-rw-rw-r-- 1 dimas dimas 872 Nov 21 23:04 output/laporan.txt
```

**Status:** LULUS (laporan terbentuk dan memuat status smbd, backup, hasil uji akses, serta log operasional)

**Catatan temuan:** Pada bagian "Backup terakhir", baris `Verifikasi checksum` menampilkan "GAGAL atau berkas checksum tidak ada", padahal berkas `.sha256` untuk backup tersebut ada. Kemungkinan penyebabnya, berkas backup dan checksum dimiliki `root` dengan izin `-rw-r-----`, sedangkan `report.sh` dijalankan sebagai user biasa (tanpa `sudo`) sehingga tidak bisa membacanya. Hal ini perlu dicek lebih lanjut (misalnya dengan menjalankan `sudo bash scripts/report.sh`).

---

## Langkah 4: Bukti integritas laporan

### 4a. Simpan hash sebelum uji

```bash
sha256sum output/laporan.txt > evidence/laporan.sha256.before
cat evidence/laporan.sha256.before
```

**Hasil:**

```
81cb77b4324996b6e602f6280b339d1d7951138ad1e3d84e3c9e0eee57e506b1  output/laporan.txt
```

### 4b. Baca lewat container read-only (harus berhasil)

```bash
sudo docker run --rm \
  --mount type=bind,src="$(pwd)/output",dst=/data,readonly \
  "$IMAGE" cat /data/laporan.txt
echo "exit=$?"
```

**Harapan:** isi laporan tampil dan `exit=0`.

**Hasil:** Isi `laporan.txt` tampil lengkap di terminal, sama dengan isi pada langkah 3, diikuti:

```
exit=0
```

**Status:** LULUS

### 4c. Coba ubah laporan (harus gagal)

```bash
sudo docker run --rm \
  --mount type=bind,src="$(pwd)/output",dst=/data,readonly \
  "$IMAGE" sh -c 'echo "uji perubahan" >> /data/laporan.txt'
echo "exit=$?"
```

**Harapan:** muncul pesan "Read-only file system" dan exit bukan 0.

**Hasil:**

```
sh: can't create /data/laporan.txt: Read-only file system
exit=1
```

**Status:** LULUS

### 4d. Verifikasi hash sesudah uji

```bash
sha256sum -c evidence/laporan.sha256.before
```

**Harapan:** `output/laporan.txt: OK`.

**Hasil:**

```
output/laporan.txt: OK
```

**Status:** LULUS

---

## Ringkasan Hasil

| No | Pengujian | Harapan | Hasil | Status |
|----|-----------|---------|-------|--------|
| 1a | fs-check saat smbd hidup | exit=0 | exit=0 | LULUS |
| 1b | fs-check saat smbd mati | exit=1 | exit=1 | LULUS |
| 1c | fs-check saat smbd pulih | exit=0 | exit=0 | LULUS |
| 2 | Pencatatan hasil uji akses | Entri T3-N tercatat | Entri tercatat | LULUS |
| 3 | Pembuatan laporan | laporan.txt terbentuk | Terbentuk (872 byte) | LULUS |
| 4b | Baca via container read-only | Berhasil, exit=0 | Berhasil, exit=0 | LULUS |
| 4c | Ubah via container read-only | Gagal, Read-only file system | Gagal, exit=1 | LULUS |
| 4d | Verifikasi hash | laporan.txt: OK | laporan.txt: OK | LULUS |

## Kesimpulan

Seluruh pengujian sesuai harapan. `fs-check.sh` mendeteksi status smbd dengan benar (exit 0 saat hidup, exit 1 saat mati, dan kembali 0 setelah dipulihkan), hasil uji akses tercatat di `access-tests.log`, dan laporan berhasil dibuat. Integritas laporan terbukti: container read-only bisa membaca laporan tetapi tidak bisa mengubahnya, dan hash SHA-256 sebelum dan sesudah uji tetap sama.

Satu temuan yang perlu ditindaklanjuti: verifikasi checksum backup di laporan menampilkan "GAGAL atau berkas checksum tidak ada" (lihat catatan pada langkah 3).
