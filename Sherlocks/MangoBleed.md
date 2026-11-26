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
Ans: 
