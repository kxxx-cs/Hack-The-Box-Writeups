# Editing Files

**1. What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?**
**SSH to <IP Address> (ACADEMY-NIXFUND), with user "htb-student" and password "HTB_@cademy_stdnt!"**

Ans: 00-mesa-defaults.conf

Solution:

```bash
htb-student@nixfund:~$ find / -type f -name *.conf -size +25k -size -28k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null
-rw-r--r-- 1 root root 27422 Jun 12  2020 /usr/share/drirc.d/00-mesa-defaults.conf
```

-------------------------------------------------------------------------------------------------------------------------------

**2. How many files exist on the system that have the ".bak" extension?**

Ans: 4

Solution 1:

```bash
htb-student@nixfund:~$ locate *.bak
/var/backups/group.bak
/var/backups/gshadow.bak
/var/backups/passwd.bak
/var/backups/shadow.bak
```

Solution 2:

```bash
htb-student@nixfund:~$ locate *.bak | wc -l
4
```

-------------------------------------------------------------------------------------------------------------------------------

**3. Submit the full path of the "xxd" binary.**

Ans: /usr/bin/xxd

Solution:

```bash
htb-student@nixfund:~$ locate xxd
/usr/bin/xxd
```
