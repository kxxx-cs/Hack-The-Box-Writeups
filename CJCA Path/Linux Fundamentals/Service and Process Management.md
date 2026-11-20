# Service and Process Management

**1. Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.**

Ans: snapd.apparmor.service

Solution:

```bash
htb-student@nixfund:~$ systemctl list-units --type=service | grep -I "Load AppArmor profiles managed internally by snapd"
snapd.apparmor.service               loaded active exited  Load AppArmor profiles managed internally by snapd 
```
