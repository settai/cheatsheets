# Gobuster

gobuster dir -u http://<ip>:<port> -w <wordlist path> -t 30

* -u	The target URL
* -e	Print the full URLs in your console
* -w	Path to your wordlist Kali "/usr/share/wordlistsdirb/common.txt"
* -x	Set extension
* -p <x>	Proxy to use for requests
* -c <http cookies>	Specify a cookie for simulating your auth
* -t	Number of concurrent threads
* -U and -P	Username and Password for Basic Auth
* -s <status>	status code interpreted as valid
* -k	skip ssl certificate verification
* -a	specify User-Agent
* -h	specify HTTP header
