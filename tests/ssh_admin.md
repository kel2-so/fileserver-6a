mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ ssh adm1@localhost

The authenticity of host 'localhost (127.0.0.1)' can't be established.

ED25519 key fingerprint is: SHA256:1cm+9qgm7IucbgS1W/KXkZlBDk7dgJ2pln5mL6R33tY

This key is not known by any other names.

Are you sure you want to continue connecting (yes/no/\[fingerprint])? yes

Warning: Permanently added 'localhost' (ED25519) to the list of known hosts.

adm1@localhost's password: 

Welcome to Ubuntu 26.04.1 LTS (GNU/Linux 7.0.0-42-generic x86\_64)
&#x20;\* Documentation:  https://docs.ubuntu.com

&#x20;\* Management:     https://landscape.canonical.com

&#x20;\* Support:        https://ubuntu.com/pro



Expanded Security Maintenance for Applications is not enabled.



0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.

See https://ubuntu.com/esm or run: sudo pro status



Last login: Fri Nov  6 19:39:54 2026 from 192.168.1.10

adm1@mario-dionisius-pake-VirtualBox:\~$ whoami

adm1

adm1@mario-dionisius-pake-VirtualBox:\~$ sudo systemctl status smbd
\[sudo: authenticate] Password:             

sudo: Authentication failed, try again.

\[sudo: authenticate] Password:             

sudo: Authentication failed, try again.

\[sudo: authenticate] Password:             

sudo: maximum 3 incorrect authentication attempts

adm1@mario-dionisius-pake-VirtualBox:\~$ sudo systemctl status smbd

\[sudo: authenticate] Password:             

sudo: Authentication failed, try again.

\[sudo: authenticate] Password:               

● smbd.service - Samba SMB Daemon
#x20;    Loaded: loaded (/usr/lib/systemd/system/smbd.service; enabled; preset: enabled)

&#x20;    Active: active (running) since Wed 2026-11-18 12:36:54 WIB; 1h 15min ago

&#x20;Invocation: abde2d0524d34e2e8f2a3b1a4e30237b

&#x20;      Docs: man:smbd(8)

&#x20;            man:samba(7)

&#x20;            man:smb.conf(5)
&#x20;   Process: 11339 ExecCondition=/usr/share/samba/is-configured smb (code=exited, status=0/SUCCESS)

&#x20;   Process: 11341 ExecStartPre=/usr/share/samba/update-apparmor-samba-profile (code=exited, status=0/SUCCESS)

&#x20;  Main PID: 11347 (smbd)

&#x20;    Status: "smbd: ready to serve connections..."

&#x20;     Tasks: 5 (limit: 1856)

&#x20;    Memory: 20.9M (peak: 98.3M, swap: 4.9M, swap peak: 6M)

&#x20;       CPU: 3.963s

&#x20;    CGroup: /system.slice/smbd.service
&#x20;            ├─11347 /usr/sbin/smbd --foreground --no-process-group

&#x20;            ├─11349 "smbd: notifyd" .

&#x20;            ├─11351 "smbd: cleanupd "

&#x20;            ├─12073 "smbd: client \[192.168.110.73]"

&#x20;            └─13272 "smbd: client \[192.168.110.134]"
Nov 18 13:37:21 mario-dionisius-pake-VirtualBox smbd\[13216]: pam\_unix(samba:session): session closed for user op1

Nov 18 13:37:31 mario-dionisius-pake-VirtualBox smbd\[13251]: pam\_unix(samba:session): session opened for user op1(uid=1002) by (uid=0)

Nov 18 13:39:03 mario-dionisius-pake-VirtualBox smbd\[13251]: pam\_unix(samba:session): session closed for user op1

Nov 18 13:39:10 mario-dionisius-pake-VirtualBox smbd\[13272]: pam\_unix(samba:session): session opened for user op1(uid=1002) by (uid=0)

Nov 18 13:43:15 mario-dionisius-pake-VirtualBox smbd\[13383]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

Nov 18 13:43:35 mario-dionisius-pake-VirtualBox smbd\[13383]: pam\_unix(samba:session): session closed for user rd1

Nov 18 13:44:03 mario-dionisius-pake-VirtualBox smbd\[13395]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

Nov 18 13:45:27 mario-dionisius-pake-VirtualBox smbd\[13395]: pam\_unix(samba:session): session closed for user rd1

Nov 18 13:47:33 mario-dionisius-pake-VirtualBox smbd\[13485]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

Nov 18 13:48:17 mario-dionisius-pake-VirtualBox smbd\[13485]: pam\_unix(samba:session): session closed for user rd1
adm1@mario-dionisius-pake-VirtualBox:\~$ sudo /usr/local/sbin/fs-backup.sh

Backup selesai: backup\_20261118\_135307.tar.gz

adm1@mario-dionisius-pake-VirtualBox:\~$ exit

logout

Connection to localhost closed.

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ ssh op1@localhost

op1@localhost's password: 

Welcome to Ubuntu 26.04.1 LTS (GNU/Linux 7.0.0-42-generic x86\_64)

&#x20;\* Documentation:  https://docs.ubuntu.com

&#x20;\* Management:     https://landscape.canonical.com

&#x20;\* Support:        https://ubuntu.com/pro



Expanded Security Maintenance for Applications is not enabled.



0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.

See https://ubuntu.com/esm or run: sudo pro status



Last login: Fri Nov  6 19:39:54 2026 from 192.168.1.10

adm1@mario-dionisius-pake-VirtualBox:\~$ whoami

adm1

adm1@mario-dionisius-pake-VirtualBox:\~$ sudo systemctl status smbd

\[sudo: authenticate] Password:             

sudo: Authentication failed, try again.

\[sudo: authenticate] Password:             

sudo: Authentication failed, try again.

\[sudo: authenticate] Password:             

sudo: maximum 3 incorrect authentication attempts

adm1@mario-dionisius-pake-VirtualBox:\~$ sudo systemctl status smbd

\[sudo: authenticate] Password:             

sudo: Authentication failed, try again.

\[sudo: authenticate] Password:               

● smbd.service - Samba SMB Daemon

&#x20;    Loaded: loaded (/usr/lib/systemd/system/smbd.service; enabled; preset: enabled)

&#x20;    Active: active (running) since Wed 2026-11-18 12:36:54 WIB; 1h 15min ago

&#x20;Invocation: abde2d0524d34e2e8f2a3b1a4e30237b

&#x20;      Docs: man:smbd(8)

&#x20;            man:samba(7)

&#x20;            man:smb.conf(5)

&#x20;   Process: 11339 ExecCondition=/usr/share/samba/is-configured smb (code=exited, status=0/SUCCESS)

&#x20;   Process: 11341 ExecStartPre=/usr/share/samba/update-apparmor-samba-profile (code=exited, status=0/SUCCESS)

&#x20;  Main PID: 11347 (smbd)

&#x20;    Status: "smbd: ready to serve connections..."

&#x20;     Tasks: 5 (limit: 1856)

&#x20;    Memory: 20.9M (peak: 98.3M, swap: 4.9M, swap peak: 6M)

&#x20;       CPU: 3.963s

&#x20;    CGroup: /system.slice/smbd.service

&#x20;            ├─11347 /usr/sbin/smbd --foreground --no-process-group

&#x20;            ├─11349 "smbd: notifyd" .

&#x20;            ├─11351 "smbd: cleanupd "

&#x20;            ├─12073 "smbd: client \[192.168.110.73]"

&#x20;            └─13272 "smbd: client \[192.168.110.134]"
Nov 18 13:37:21 mario-dionisius-pake-VirtualBox smbd\[13216]: pam\_unix(samba:session): session closed for user op1

Nov 18 13:37:31 mario-dionisius-pake-VirtualBox smbd\[13251]: pam\_unix(samba:session): session opened for user op1(uid=1002) by (uid=0)

Nov 18 13:39:03 mario-dionisius-pake-VirtualBox smbd\[13251]: pam\_unix(samba:session): session closed for user op1

Nov 18 13:39:10 mario-dionisius-pake-VirtualBox smbd\[13272]: pam\_unix(samba:session): session opened for user op1(uid=1002) by (uid=0)

Nov 18 13:43:15 mario-dionisius-pake-VirtualBox smbd\[13383]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

Nov 18 13:43:35 mario-dionisius-pake-VirtualBox smbd\[13383]: pam\_unix(samba:session): session closed for user rd1

Nov 18 13:44:03 mario-dionisius-pake-VirtualBox smbd\[13395]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

Nov 18 13:45:27 mario-dionisius-pake-VirtualBox smbd\[13395]: pam\_unix(samba:session): session closed for user rd1

Nov 18 13:47:33 mario-dionisius-pake-VirtualBox smbd\[13485]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

Nov 18 13:48:17 mario-dionisius-pake-VirtualBox smbd\[13485]: pam\_unix(samba:session): session closed for user rd1

adm1@mario-dionisius-pake-VirtualBox:\~$ sudo /usr/local/sbin/fs-backup.sh

Backup selesai: backup\_20261118\_135307.tar.gz

adm1@mario-dionisius-pake-VirtualBox:\~$ exit

logout

Connection to localhost closed.
mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ ssh op1@localhost

op1@localhost's password: 

Welcome to Ubuntu 26.04.1 LTS (GNU/Linux 7.0.0-42-generic x86\_64)



&#x20;\* Documentation:  https://docs.ubuntu.com

&#x20;\* Management:     https://landscape.canonical.com

&#x20;\* Support:        https://ubuntu.com/pro



Expanded Security Maintenance for Applications is not enabled.



0 updates can be applied immediately.



Enable ESM Apps to receive additional future security updates.

See https://ubuntu.com/esm or run: sudo pro status

The programs included with the Ubuntu system are free software;

the exact distribution terms for each program are described in the

individual files in /usr/share/doc/\*/copyright.



Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by

applicable law.



op1@mario-dionisius-pake-VirtualBox:\~$ whoami

op1

op1@mario-dionisius-pake-VirtualBox:\~$ sudo /usr/local/sbin/fs-backup.sh

sudo: I'm sorry op1. I'm afraid I can't do that
