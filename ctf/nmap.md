# Nmap

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
