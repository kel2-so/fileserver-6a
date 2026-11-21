**TESTING POSITIF NEGATIF SAMBA SERVER:**

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ sudo systemctl status smbd

● smbd.service - Samba SMB Daemon

&#x20;    Loaded: loaded (/usr/lib/systemd/system/smbd.service; enabled; preset: enabled)

&#x20;    Active: active (running) since Wed 2026-11-18 12:36:54 WIB; 47min ago

&#x20;Invocation: abde2d0524d34e2e8f2a3b1a4e30237b

&#x20;      Docs: man:smbd(8)

&#x20;            man:samba(7)

&#x20;            man:smb.conf(5)

&#x20;   Process: 11339 ExecCondition=/usr/share/samba/is-configured smb (code=exited, status=0/SUCCESS)

&#x20;   Process: 11341 ExecStartPre=/usr/share/samba/update-apparmor-samba-profile (code=exited, status=0/SUCCESS)

&#x20;  Main PID: 11347 (smbd)

&#x20;    Status: "smbd: ready to serve connections..."

&#x20;     Tasks: 4 (limit: 1856)

&#x20;    Memory: 14.2M (peak: 98.3M, swap: 5.8M, swap peak: 6M)

&#x20;       CPU: 1.484s

&#x20;    CGroup: /system.slice/smbd.service

&#x20;            ├─11347 /usr/sbin/smbd --foreground --no-process-group

&#x20;            ├─11349 "smbd: notifyd" .

&#x20;            ├─11351 "smbd: cleanupd "

&#x20;            └─12073 "smbd: client \[192.168.110.73]"



Nov 18 12:36:53 mario-dionisius-pake-VirtualBox systemd\[1]: Starting smbd.service - Samba SMB Daemon...

Nov 18 12:36:54 mario-dionisius-pake-VirtualBox systemd\[1]: Started smbd.service - Samba SMB Daemon.

Nov 18 13:07:15 mario-dionisius-pake-VirtualBox smbd\[12073]: pam\_unix(samba:session): session opened for user rd1(uid=1004) by (uid=0)

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ testparm -s

Load smb config files from /etc/samba/smb.conf

Loaded services file OK.

Weak crypto is allowed by GnuTLS (e.g. NTLM as a compatibility fallback)



WARNING: The 'netbios name' is too long (max. 15 chars).



Server role: ROLE\_STANDALONE



\# Global parameters

\[global]

&#x09;disable netbios = Yes

&#x09;log file = /var/log/samba/log.%m

&#x09;logging = file

&#x09;map to guest = Bad User

&#x09;max log size = 1000

&#x09;obey pam restrictions = Yes

&#x09;pam password change = Yes

&#x09;panic action = /usr/share/samba/panic-action %d

&#x09;passwd chat = \*Enter\\snew\\s\*\\spassword:\* %n\\n \*Retype\\snew\\s\*\\spassword:\* %n\\n \*password\\supdated\\ssuccessfully\* .

&#x09;passwd program = /usr/bin/passwd %u

&#x09;server role = standalone server

&#x09;server signing = if\_required

&#x09;server string = %h server (Samba, Ubuntu)

&#x09;unix password sync = Yes

&#x09;usershare allow guests = Yes

&#x09;idmap config \* : backend = tdb





\[printers]

&#x09;browseable = No

&#x09;comment = All Printers

&#x09;create mask = 0700

&#x09;path = /var/tmp

&#x09;printable = Yes





\[print$]

&#x09;comment = Printer Drivers

&#x09;path = /var/lib/samba/printers





\[berkas]

&#x09;create mask = 0660

&#x09;directory mask = 02770

&#x09;path = /srv/fileserver/share

&#x09;read list = @sf\_reader

&#x09;valid users = @sf\_operator @sf\_reader op1

&#x09;write list = @sf\_operator

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ smbclient -L localhost -U op1

Password for \[WORKGROUP\\op1]:



&#x09;Sharename       Type      Comment

&#x09;---------       ----      -------

&#x09;print$          Disk      Printer Drivers

&#x09;berkas          Disk      

&#x09;IPC$            IPC       IPC Service (mario-dionisius-pake-VirtualBox server (Samba, Ubuntu))

SMB1 disabled -- no workgroup available

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ smbclient -L localhost -U tamu1

Password for \[WORKGROUP\\tamu1]:



&#x09;Sharename       Type      Comment

&#x09;---------       ----      -------

&#x09;print$          Disk      Printer Drivers

&#x09;berkas          Disk      

&#x09;IPC$            IPC       IPC Service (mario-dionisius-pake-VirtualBox server (Samba, Ubuntu))

SMB1 disabled -- no workgroup available

mario-dionisius-pake@mario-dionisius-pake-VirtualBox:\~/Downloads/proyek-6a$ smbclient --version

Version 4.23.6-Ubuntu-4.23.6+dfsg-1ubuntu2.2
