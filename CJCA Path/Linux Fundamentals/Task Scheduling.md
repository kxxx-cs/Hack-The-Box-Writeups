# Task Scheduling

**1. What is the Type of the service of the "dconf.service"?**

Ans: dbus

Solution:

```bash
htb-student@nixfund:~$ dpkg -l | grep dconf
ii  dconf-gsettings-backend:amd64          0.26.0-2ubuntu3                                 amd64        simple configuration storage system - GSettings back-end
ii  dconf-service                          0.26.0-2ubuntu3                                 amd64        simple configuration storage system - D-Bus service
ii  libdconf1:amd64                        0.26.0-2ubuntu3                                 amd64        simple configuration storage system - runtime library
```
