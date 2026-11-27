# User and Group Management

1. What resource can provide Windows environments with directory services to manage users, computers, and more? (full name not abbreviation)
Ans: Active Directory

---

2. What PowerShell Cmdlet will display all LOCAL users on a host?
Ans: Get-LocalUser

Solution:

```bash
PS C:\Users\htb-student\Desktop> Get-LocalUser

Name               Enabled Description                                                                                    
----               ------- -----------
Administrator      True    Built-in account for administering the computer/domain
DefaultAccount     False   A user account managed by the system.
Guest              False   Built-in account for guest access to the computer/domain
htb-student        True
WDAGUtilityAccount False   A user account managed and used by the system for Windows Defender Application Guard scenarios.
```

---

3. Connect to the target host and search for a domain user with the given name of Robert. What is this users Surname?
Ans: Loxley

Solution:

```bash

```
