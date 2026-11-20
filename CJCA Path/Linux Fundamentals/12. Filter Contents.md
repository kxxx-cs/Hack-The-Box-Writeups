# Filter Contents

**1. How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)**

Ans: 7

Solution:

```bash
htb-student@nixfund:~$ netstat -ln4 | grep LISTEN | grep -v 127 | wc -l
7
```

-------------------------------------------------------------------------------------------------------------------------------

**2. Determine what user the ProFTPd server is running under. Submit the username as the answer.**

Ans: proftpd

Solution:

```bash
htb-student@nixfund:~$ ps aux | grep proftpd
proftpd   1761  0.0  0.1 126444  3684 ?        Ss   02:33   0:00 proftpd: (accepting connections)
htb-stu+  2258  0.0  0.0  13144  1040 pts/0    S+   02:34   0:00 grep --color=auto proftpd

htb-student@nixfund:~$ grep proftpd /etc/passwd
proftpd:x:112:65534::/run/proftpd:/usr/sbin/nologin
```

----------------------------------------------------------------------------------------------------------------------------

**3. Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths (https://www.inlanefreight.com/directory" or "/another/directory") of that domain. Submit the number of these paths as the answer.**

Ans: 34

Solution:

```bash
┌──(kali㉿kali)-[~/htb]
└─$ curl https://www.inlanefreight.com | tr " " "\n" | cut -d"'" -f2 | cut -d'"' -f2 | grep www.inlanefreight.com | sort -u | wc -l
  % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
100  22266   0  22266   0      0  16079      0           00:01              0
34
```
