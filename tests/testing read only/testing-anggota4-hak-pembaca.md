# Testing Hak Pembaca (Read-Only)

## Tujuan
Membuktikan bahwa akun pembaca (`rd1`) hanya dapat **membaca dan mengunduh** dokumen, tetapi **tidak dapat mengubah maupun menghapusnya**.

## Lingkungan Pengujian
| Item | Keterangan |
|---|---|
| Server | Ubuntu (VirtualBox), IP `192.168.1.48` |
| Shared folder | `/srv/fileserver/share` (nama share: `berkas`) |
| Akun uji | `rd1` (grup `sf_reader`) |
| Client | Linux (`smbclient`) dan Windows (File Explorer) |

## Konfigurasi Hak Akses
Perintah:
```bash
getfacl /srv/fileserver/share
```

![Hasil getfacl](images/anggota4/02-getfacl.png)

Grup `sf_reader` hanya memiliki izin `r-x` (baca), sedangkan `sf_operator` memiliki `rwx`.

---

## A. Testing Positif — Pembaca Dapat Melihat Dokumen
**Perintah:**
```bash
smbclient //localhost/berkas -U rd1
ls
get dokumen1.txt /tmp/dokumen1.txt
exit
cat /tmp/dokumen1.txt
```

**Hasil:**

<!-- TODO: tempel screenshot / output terminal -->
![Pembaca melihat dan mengunduh dokumen](images/anggota4/A-baca-unduh.png)

**Hasil yang diharapkan:** isi dokumen berhasil ditampilkan.
**Status:** Berhasil

---

## B. Testing Negatif — Pembaca Tidak Dapat Mengunggah File
**Perintah:**
```bash
smbclient //localhost/berkas -U rd1
put /etc/hostname gagal.txt
```

**Hasil:**
```
NT_STATUS_ACCESS_DENIED
```

<!-- TODO: tempel screenshot -->
![Upload ditolak](images/anggota4/B-upload-ditolak.png)

**Status:** Sesuai harapan (ditolak)

---

## C. Testing Negatif — Pembaca Tidak Dapat Menghapus Dokumen
**Perintah (masih di dalam smbclient):**
```bash
del dokumen1.txt
exit
```

**Hasil:**
```
NT_STATUS_ACCESS_DENIED
```

<!-- TODO: tempel screenshot -->
![Hapus ditolak](images/anggota4/C-hapus-ditolak.png)

**Status:** Sesuai harapan (ditolak)

---

## D. Verifikasi Dokumen Tidak Berubah
**Perintah:**
```bash
sudo ls -l /srv/fileserver/share/
```

![Isi folder share](images/anggota4/01-ls-permission.png)

`dokumen1.txt` masih ada dan `gagal.txt` tidak terbentuk.

**Status:** Berhasil

---

## E. Pengujian Tambahan dari Windows (File Explorer)
Koneksi ke share dengan akun pembaca:
```cmd
net use * /delete
net use \\192.168.1.48\berkas /user:rd1
start \\192.168.1.48\berkas
```

Saat pembaca mencoba menambah/mengubah file, Windows menampilkan pesan akses ditolak:

![Destination Folder Access Denied](images/anggota4/03-windows-dest-folder-denied.png)

![File Access Denied saat mengubah file](images/anggota4/04-windows-file-access-denied.png)

![File Access Denied saat rename](images/anggota4/05-windows-rename-denied.png)

Pesan menyebutkan bahwa perubahan memerlukan izin dari pemilik file (`Unix User\root`), sehingga akun pembaca tidak dapat mengubah file.

---

## Ringkasan Hasil
| No | Skenario | Hasil yang Diharapkan | Hasil Aktual | Status |
|---|---|---|---|---|
| 1 | Lihat & unduh dokumen | Berhasil | Berhasil | berhasil |
| 2 | Upload file | `NT_STATUS_ACCESS_DENIED` | `NT_STATUS_ACCESS_DENIED` | berhasil |
| 3 | Hapus dokumen | `NT_STATUS_ACCESS_DENIED` | `NT_STATUS_ACCESS_DENIED` | berhasil |
| 4 | Dokumen tetap utuh | Tidak berubah | Tidak berubah | berhasil |
