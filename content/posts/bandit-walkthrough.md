---
lastmod: 2022-08-09
title: "Bandit Wargame Walkthrough"
tags: ["hacking", "linux", "cybersecurity", "walkthrough", "writeup", "ctf"]
date: 2022-03-29
description: "Spoilers within!"
type: "post"
weight: 10
showTableOfContents: true
---

[This page is licensed under a Creative Commons Attribution-NoDerivatives 4.0 International License.]: # 

# Introduction {#introduction}

The Bandit wargame by OverTheWire teaches the basics of Linux. It can be [played here](https://overthewire.org/wargames/bandit/).

This write-up gives a single solution to each level.

# Walkthrough {#walkthrough}

## Level 0 {#level-0}

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

## Level 1 {#level-1}

```bash
cat readme
```

## Level 2 {#level-2}

The `-` character is interpreted as standard input by the shell.

Use redirection to read the file.

```bash
cat < -
```

## Level 3 {#level-3}

Encapsulate the file name with quotation marks or backslashes.

```bash
cat 'spaces in this filename'
cat spaces\ in\ this\ filename
```

## Level 4 {#level-4}

Hidden files are prefixed by the `.` character.

```bash
ls -A inhere/

cat inhere/.hidden
```

## Level 5 {#level-5}

Iterate through the file numbers.

```bash
cat < -file07
```

## Level 6 {#level-6}

List all entries (`-A`) recursively (`-R`), including permission bits and file size (`-l`).

The subdirectory isn't visible when using `grep`, so output is piped to `less`.

```bash
ls -lAR inhere/ | less
```

Search for `1033`.

```bash
cat inhere/maybehere07/.file2
```

## Level 7 {#level-7}

Redirect standard error to discard **Permission denied** messages.

```bash
find / -user bandit7 -group bandit6 -size 33c 2> /dev/null
```

## Level 8 {#level-8}

```bash
grep millionth data.txt
```

## Level 9 {#level-9}

Strings must be sorted alphabetically before being searched for unique lines.

```bash
sort -d data.txt | uniq -u
```

## Level 10 {#level-10}

Search for character sequences amongst the binary garbage.

```bash
strings data.txt | grep ==
```

## Level 11 {#level-11}

```bash
base64 -d data.txt 
```

## Level 12 {#level-12}

The ROT13 cipher is encrypted and decrypted the same way, by shifting the characters 13 places.

```bash
cat data.txt | tr 'N-ZA-Mn-za-m' 'A-Za-z' 
```

## Level 13 {#level-13}

* Convert the hexdump into binary

```bash
xxd -r data.txt binary.txt
```

* Determine the file types
* Rename the file to include the extension
* Decompress the archives

```bash
file binary.txt 

mv binary.txt binary.txt.gz
gunzip binary.txt.gz
```

The file name and `.txt` extension are of no consequence, but the `.gz`, `.bz2` and `.tar` extensions are required by `gunzip`, `bunzip2` and `tar` respectively.

One pass of the procedure is listed above. More are needed to complete the level.

## Level 14 {#level-14}

Copy the private key to the client machine.

* Modify file permissions
* Use the private key for public key authentication

```bash
chmod 400 /path/to/sshkey.private
ssh -p 2220 -i /path/to/sshkey.private bandit14@bandit.labs.overthewire.org
```

## Level 15 {#level-15}

Connect and provide the password.

```bash
cat /etc/bandit_pass/bandit14 

telnet localhost 30000
```

## Level 16 {#level-16}

Connect and provide the password.

```bash
openssl s_client -connect localhost:30001
```

## Level 17 {#level-17}

* Scan ports in the range
* Probe for service information to find the SSL ports
* Connect and provide the password

```bash
nmap -p 31000-32000 localhost

nmap -T5 -sV -p 31046,31518,31691,31790,31960 localhost

openssl s_client -connect localhost:31790
```

## Level 18 {#level-18}

```bash
diff passwords.old passwords.new
```

## Level 19 {#level-19}

Issue a command when connecting to find the password.

```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org cat readme
```

## Level 20 {#level-20}

Files in `/etc/bandit_pass` are owned by their respective user.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20 
```

## Level 22 {#level-22}

The user's `crontab` writes the contents of their password file to a file readable by everyone in `/tmp`.

```bash
cat /etc/cron.d/cronjob_bandit22

cat /usr/bin/cronjob_bandit22.sh 
```

## Level 23 {#level-23}

The user's `crontab` writes the contents of their password file to a file readable by everyone in `/tmp`.

```bash
cat /etc/cron.d/cronjob_bandit23 

cat /usr/bin/cronjob_bandit23.sh 

echo I am user bandit23 | md5sum | cut -d ' ' -f 1

cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

## Level 24 {#level-24}

The `crontab` runs every minute, executes scripts in `/var/spool/bandit24`, then removes them. If the script is owned by `bandit23`, it waits 60 seconds to kill the script.

1. Write this oneliner to a script and make it executable.

```bash
vi 24.sh
chmod +x 24.sh
```

```bash
#! /usr/bin/env bash

cat /etc/bandit_pass/bandit24 | tee /tmp/path/bandit24
```

2. Replace `/tmp/path` with whatever was created by `mktemp -d`
3. Copy `24.sh` to `/var/spool/bandit24` and wait for the next minute

## Level 25 {#level-25}

```bash
#! /usr/bin/env dash

# Execute the script, then pipe to telnet
# /path/to/script | telnet $host $port

# Wait for a telnet prompt
sleep 1

# Iterate i from 0 to 10000 to brute force the PIN
n=0
while [ $n -le 10000 ]
do
    echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $n"
    n=$((n + 1))
    # telnet closes the connection if there is no wait period between attempts
    sleep .1
done
```

## Level 27 {#level-27}

Files in `/etc/bandit_pass` are owned by their respective user.

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

## Level 28 {#level-28}

Create a new directory with `mktemp -d` and replace `/tmp/path` with its name.

```bash
git clone ssh://bandit27-git@localhost/home/bandit27-git/repo /tmp/path

cd /tmp/path
cat README 
```

## Level 29 {#level-29}

View changes made to the file.

```bash
git log -p
```

## Level 30 {#level-30}

Switch to a different branch.

```bash
git branch -a

git log -p
```

## Level 32 {#level-32}

Remove `.gitignore` to permit the addition of `key.txt`.

```bash
cat README.md 

echo 'May I come in?' > key.txt

git rm .gitignore

git add key.txt

git commit

git push
```
