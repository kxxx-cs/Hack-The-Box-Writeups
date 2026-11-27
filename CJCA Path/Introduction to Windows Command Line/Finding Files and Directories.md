# Finding Files and Directories

**1. What command can be used to search for regular expression strings from command prompt?**\
Ans: findstr

Solution:

```bash
PS C:\Users\htb\Desktop> findstr /c:"testing" "New Text Document.txt"
testing file for htb
```

---

**2. Using the skills acquired in this and previous sections, access the target host and search for the file named 'waldo.txt'. Submit the flag found within the file.**\
Ans: RmxhZ3MgYXJlbid0IGhhcmQgdG8gZmluZCBub3csIHJpZ2h0Pw==

Solution:

```bash
PS C:\Users\htb-student\Desktop> Get-ChildItem -Path "C:\" -Filter "waldo.txt" -Recurse -File -ErrorAction SilentlyContinue  


    Directory: C:\Users\MTanaka\Favorites


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         11/9/2022  11:31 AM            110 waldo.txt

PS C:\Users\htb-student\Desktop> type C:\Users\MTanaka\Favorites\waldo.txt
RmxhZ3MgYXJlbid0IGhhcmQgdG8gZmluZCBub3csIHJpZ2h0Pw==
```
