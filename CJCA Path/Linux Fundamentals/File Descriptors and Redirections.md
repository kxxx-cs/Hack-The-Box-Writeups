# File Descriptors and Redirections

**1. How many files exist on the system that have the ".log" file extension?**
**SSH to <IP Address> (ACADEMY-NIXFUND), with user "htb-student" and password "HTB_@cademy_stdnt!"**

Ans: 32

Solution:

```bash
htb-student@nixfund:~$ find / -type f -name *.log 2>/dev/null | wc -l
32
```

-------------------------------------------------------------------------------------------------------------------------------

**2. How many total packages are installed on the target system?**

Ans: 737

Solution:

```bash
htb-student@nixfund:~$ dpkg -l | grep -c '^ii'
737
```
