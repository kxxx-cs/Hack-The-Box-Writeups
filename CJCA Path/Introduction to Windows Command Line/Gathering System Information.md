# Gathering System Information

**1. What command will output verbose system information such as OS configuration, security info, hardware info, and more?**\
Ans: systeminfo

Solution:

```bash
PS C:\Users\htb-student\Desktop> systeminfo
                                                                              
Host Name:                 ICL-WIN11
OS Name:                   Microsoft Windows 11 Pro
OS Version:                10.0.22000 N/A Build 22000
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Member Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          htb-student
Registered Organization:
Product ID:                00331-20309-59368-AA170
Original Install Date:     6/14/2022, 7:21:28 PM
System Boot Time:          11/26/2026, 5:08:33 PM
System Manufacturer:       VMware, Inc.
System Model:              VMware7,1
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: AMD64 Family 25 Model 1 Stepping 1 AuthenticAMD ~2445 Mhz
BIOS Version:              VMware, Inc. VMW71.00V.24504846.B64.2501180334, 1/18/2025
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC-08:00) Pacific Time (US & Canada)
Total Physical Memory:     4,095 MB
Available Physical Memory: 2,414 MB
Virtual Memory: Max Size:  4,799 MB
Virtual Memory: Available: 3,471 MB
Virtual Memory: In Use:    1,328 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    greenhorn.corp
Logon Server:              N/A
Hotfix(s):                 4 Hotfix(s) Installed.
                           [01]: KB5020617
                           [02]: KB5012170
                           [03]: KB5019961
                           [04]: KB5017850
Network Card(s):           2 NIC(s) Installed.
                           [01]: vmxnet3 Ethernet Adapter
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    Yes
                                 DHCP Server:     10.10.10.2
                                 IP address(es)
                                 [01]: 10.129.203.105
                                 [02]: fe80::d9e6:d1c7:ca1:62eb
                                 [03]: dead:beef::e150:b966:6f0d:60a6
                                 [04]: dead:beef::ac5b:92ae:b8f8:58ea
                                 [05]: dead:beef::16e
                           [02]: vmxnet3 Ethernet Adapter
                                 Connection Name: Ethernet2
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 172.16.5.100
                                 [02]: fe80::a510:7652:d68b:d1e1
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

---

**2. Access the target host and run the 'hostname' command. What is the hostname?**\
Ans: ICL-WIN11

Solution:

```bash
PS C:\Users\htb-student\Desktop> hostname
ICL-WIN11
```

