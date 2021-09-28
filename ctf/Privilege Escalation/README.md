# Privilege Escalation

[Linpeas](linpeas.md)

## Lxd Privilege Escalation

[https://www.exploit-db.com/exploits/46978](https://www.exploit-db.com/exploits/46978)

## Sudo permissions

```bash
sudo -l
```

## SUID Binaries Privilege Escalate

```bash
 find / -perm -u=s -type f 2>/dev/null
```

- **perm**	denotes search for the permissions that follow
- **u=s**  	denotes look for files that are owned by the root user
- **type**		states the type of file we are looking for
- **f**		denotes a regular file, not the directories or special files

# Capability

```bash
getcap -r / 2>/dev/null
```

## spawn bash

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

## General

https://github.com/swisskyrepo/PayloadsAllTheThings (A bunch of tools and payloads for every stage of pentesting)

## Linux:

https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/ (a bit old but still worth looking at)

https://github.com/rebootuser/LinEnum (One of the most popular priv esc scripts)

https://github.com/diego-treitos/linux-smart-enumeration/blob/master/lse.sh (Another popular script)

https://github.com/mzet-/linux-exploit-suggester (A Script that's dedicated to searching for kernel exploits)

https://gtfobins.github.io (I can not overstate the usefulness of this for priv esc, if a common binary has special permissions, you can use this site to see how to get root perms with it.)

## Windows:

https://www.fuzzysecurity.com/tutorials/16.html  (Dictates some very useful commands and methods to enumerate the host and gain intel)



https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerUp (A bit old but still an incredibly useful script)



https://github.com/411Hall/JAWS (A general enumeration script)
