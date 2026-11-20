# Working with Files and Directories

**l. What is the name of the last modified file in the "/var/backups" directory?**
**SSH to 10.129.2.219 (ACADEMY-NIXFUND), with user "htb-student" and password "HTB_@cademy_stdnt!"**

Ans: apt.extended_states.0

Solution:

```bash
htb-student@nixfund:~$ ls -lt /var/backups
total 2160
-rw-r--r-- 1 root root    41872 Nov 12  2020 apt.extended_states.0
-rw-r--r-- 1 root root     4437 Nov 12  2020 apt.extended_states.1.gz
-rw-r--r-- 1 root root   742750 Nov 11  2020 dpkg.status.0
...
htb-student@nixfund:~$
```

-------------------------------------------------------------------------------------------------------------------------------

**2. What is the inode number of the "shadow.bak" file in the "/var/backups" directory?**

Ans: 265293

Solution (refer to the inode number):

```bash
htb-student@nixfund:~$ stat /var/backups/shadow.bak
  File: /var/backups/shadow.bak
  Size: 1362            Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d      Inode: 265293      Links: 1
Access: (0600/-rw-------)  Uid: (    0/    root)   Gid: (   42/  shadow)
Access: 2020-11-12 06:25:02.359822822 +0000
Modify: 2020-09-23 22:11:07.101663506 +0000
Change: 2020-09-24 06:25:03.741470540 +0000
 Birth: -
htb-student@nixfund:~$
```
