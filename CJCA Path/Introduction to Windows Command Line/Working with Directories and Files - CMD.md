# Working with Directories and Files - CMD

**1. What command can display the contents of a file and redirect the contents of the file into another file or to the console?**\
Ans: type

Solution:

```bash
C:\Users\htb\Desktop>type "New Text Document.txt"
testing file for htb
C:\Users\htb\Desktop>
```

---

**2. What command can be used to make the 'apples' directory? (full command as answer, not the alias)**\
Ans: mkdir apples

Solution:

```bash
PS C:\Users\htb-student\Desktop> mkdir apples


    Directory: C:\Users\htb-student\Desktop


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        11/26/2026   5:37 PM                apples


PS C:\Users\htb-student\Desktop> dir


    Directory: C:\Users\htb-student\Desktop


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        11/26/2026   5:37 PM                apples   <-- The directory created                                                                           
d-----         9/28/2022   8:43 AM                Powersploit
-a----         10/5/2022  10:41 AM        5242880 AssertCompress
-a----         10/5/2022  10:43 AM         209715 ClearOut
-a----         10/5/2022  10:41 AM        5242880 ConvertFromBackup
-a----         10/5/2022  10:43 AM         209715 ConvertResize
-a----         10/5/2022  10:43 AM         209715 EditLimit
-a----         10/5/2022  10:43 AM         209715 HideDebug
-a----         10/5/2022  10:43 AM         209715 HideStart                                                                                      
-a----         9/28/2022   8:40 AM           2354 Microsoft Edge.lnk
-a----         10/5/2022  10:41 AM        5242880 MoveCompress
-a----         10/5/2022  10:41 AM        5242880 RemoveEnable
-a----         10/5/2022  10:41 AM        5242880 RemoveResize
-a----         10/5/2022  10:43 AM         209715 ResumeRead
-a----         10/5/2022  10:41 AM        5242880 SkipTest
-a----         10/5/2022  10:41 AM        5242880 StopRemove
-a----         10/5/2022  10:41 AM        5242880 UnlockUndo                                                                                     
-a----         10/5/2022  10:41 AM        5242880 WaitClose
-a----         10/5/2022  10:41 AM        5242880 WatchConfirm
-a----         10/5/2022  10:41 AM        5242880 WatchEnable
```

