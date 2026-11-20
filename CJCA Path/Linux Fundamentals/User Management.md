# User Management

**1. Which option needs to be set to create a home directory for a new user using "useradd" command?**

Ans: -m

Solution:

```bash
┌──(kali㉿kali)-[~/htb]
└─$ useradd --help                                
Usage: useradd [options] LOGIN
       useradd -D
       useradd -D [options]

Options:
...
  -m, --create-home             create the user's home directory
...
```

-------------------------------------------------------

**2. Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)**

Ans: --lock

Solution:

```bash
┌──(kali㉿kali)-[~/htb]
└─$ usermod --help
Usage: usermod [options] LOGIN

Options:
...
  -L, --lock                    lock the user account
...
```

---------------------

**3. Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)**

Ans: --command
