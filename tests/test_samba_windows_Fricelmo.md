\# Uji Samba Client dari Windows (Anggota 3)



Penguji: Fricelmo Rikar Weohawu Thalo (NIM:2510512192)

Lingkungan: Windows 11 (10.0.26200.9711), klien 192.168.1.39 (Wi-Fi) -> server Ubuntu 192.168.1.48, share `berkas`, akun `op1`.

Tanggal uji: 11/11/2026



\## Hasil uji



| ID | Tujuan | Perintah | Hasil aktual | Status |

|----|--------|----------|--------------|--------|

| T3-P0 | Konektivitas SMB | `Test-NetConnection 192.168.1.48 -Port 445` | TcpTestSucceeded : True | Lulus |

| T3-P1 | Akun berwenang mengakses share | `net use \\\\192.168.1.48\\berkas /user:op1` lalu `start \\\\192.168.1.48\\berkas` | "The command completed successfully."; folder terbuka, terlihat 5 berkas | Lulus |

| T3-N1 | Password salah ditolak | `net use \\\\192.168.1.48\\berkas /user:op1` (password salah) | "System error 86 ... The specified network password is not correct." | Lulus (ditolak) |

| T3-N2 | Tanpa kredensial valid ditolak | `net use \* /delete` lalu `start \\\\192.168.1.48\\berkas` | "Access is denied." | Lulus (ditolak) |



\## Bukti (folder evidence/)



\- `Screenshot 2026-11-11 120554.png`: Test-NetConnection port 445 (T3-P0)

\- `Screenshot 2026-11-11 120539.png`: rangkaian perintah net use, error 86, Access is denied (T3-P1, T3-N1, T3-N2)

\- `Screenshot 2026-11-11 120105.png`: isi share terlihat dari Windows (T3-P1)



\## Catatan dan keterbatasan



\- Membuka `\\\\192.168.1.48\\berkas` tanpa kredensial memunculkan pesan SMB signing. Ini dugaan: sesi tanpa akun tidak dapat menandatangani. Belum diverifikasi lewat log Samba.

\- Exit status (`%errorlevel%`) tidak tercatat saat uji.

\- Pembuatan berkas dari Windows belum didokumentasikan.

\- Akun Samba yang ada tetapi tidak berwenang belum diuji.



Pemulihan: `net use \* /delete`

