# Managing Services

**1. What command string will stop a service named 'red-light'? (full command as the answer)**\
Ans: sc stop red-light

---

**2. What Windows executable will allow us to create, query, and modify services on a host?**\
Ans: sc

Solution

```bash
PS C:\Users\htb-student\Desktop> Get-Help sc

NAME
    Set-Content

SYNTAX
    Set-Content [-Path] <string[]> [-Value] <Object[]> [-PassThru] [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Force]        
    [-Credential <pscredential>] [-WhatIf] [-Confirm] [-UseTransaction] [-NoNewline] [-Encoding {Unknown | String | Unicode | Byte |
    BigEndianUnicode | UTF8 | UTF7 | UTF32 | Ascii | Default | Oem | BigEndianUTF32}] [-Stream <string>]  [<CommonParameters>]

    Set-Content [-Value] <Object[]> -LiteralPath <string[]> [-PassThru] [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Force]   
    [-Credential <pscredential>] [-WhatIf] [-Confirm] [-UseTransaction] [-NoNewline] [-Encoding {Unknown | String | Unicode | Byte |
    BigEndianUnicode | UTF8 | UTF7 | UTF32 | Ascii | Default | Oem | BigEndianUTF32}] [-Stream <string>]  [<CommonParameters>]


ALIASES
    sc


REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It is displaying only partial help.
        -- To download and install Help files for the module that includes this cmdlet, use Update-Help.
        -- To view the Help topic for this cmdlet online, type: "Get-Help Set-Content -Online" or
           go to https://go.microsoft.com/fwlink/?LinkID=113392.
```
