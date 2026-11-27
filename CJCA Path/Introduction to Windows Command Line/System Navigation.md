# System Navigation

**1. What command will give us a listing of all files and folders in a specified path?**\
Ans: tree /F

Solution:

```bash
PS C:\Users\htb-student> tree /F
Folder PATH listing
Volume serial number is F684-763E
C:.
│   PowerView.ps1
│
├───.ssh
│       id_rsa
│       id_rsa.pub
│
├───Contacts
├───Desktop
│   │   AssertCompress
│   │   ClearOut
│   │   ConvertFromBackup
│   │   ConvertResize
│   │   EditLimit
│   │   HideDebug
│   │   HideStart
│   │   Microsoft Edge.lnk
│   │   MoveCompress
│   │   RemoveEnable
│   │   RemoveResize
│   │   ResumeRead
│   │   SkipTest
│   │   StopRemove
│   │   UnlockUndo
│   │   WaitClose
│   │   WatchConfirm
│   │   WatchEnable
│   │
│   └───Powersploit
│       └───PowerSploit-master
│           │   .gitignore
│           │   LICENSE
│           │   mkdocs.yml
│           │   PowerSploit.psd1
│           │   PowerSploit.psm1
│           │   PowerSploit.pssproj
│           │   PowerSploit.sln
│           │   README.md
...
```

---

**2. What command will print my current working directory onto the console?**\
Ans: cd

Solution:

```bash
Microsoft Windows [Version 10.0.26200.9974]
(c) Microsoft Corporation. All rights reserved.

C:\Users\htb>cd
C:\Users\htb    <-- printed current working directory

C:\Users\htb>
``
