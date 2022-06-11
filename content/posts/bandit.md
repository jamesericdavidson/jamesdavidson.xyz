---
title: "Solutions to the Bandit wargame"
date: 2022-03-29
description: "Spoilers within!"
type: "post"
---

# Introduction

Bandit teaches the basics of Linux. It can be [played here](https://overthewire.org/wargames/bandit/).

Typically, there is more than one solution to a level.

# Walkthrough

## Level 0

```
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

## Level 1

```
cat readme
```

## Level 2

The `-` character is interpreted as standard input by the shell.

Use redirection to read the file.

```
cat < -
```

## Level 3

Encapsulate the file name with quotation marks or backslashes.

```
cat 'spaces in this filename'
cat spaces\ in\ this\ filename
```

## Level 4

Hidden files are prefixed by the `.` character.

```
ls -A inhere/

cat inhere/.hidden
```

## Level 5

Iterate through the file numbers.

```
cat < -file07
```

## Level 6

List all entries (`-A`) recursively (`-R`), including permission bits and file size (`-l`).

The subdirectory isn't visible when using `grep`, so output is piped to `less`.

```
ls -lAR inhere/ | less
```

Search for `1033`.

```
cat inhere/maybehere07/.file2
```

## Level 7

Redirect standard error to discard **Permission denied** messages.

```
find / -user bandit7 -group bandit6 -size 33c 2> /dev/null
```

## Level 8

```
grep millionth data.txt
```

## Level 9

Strings must be sorted alphabetically before being searched for unique lines.

```
sort -d data.txt | uniq -u
```

## Level 10

Search for character sequences amongst the binary garbage.

```
strings data.txt | grep ==
```

## Level 11

```
base64 -d data.txt 
```

## Level 12

The ROT13 cipher is encrypted and decrypted the same way, by shifting the characters 13 places.

```
cat data.txt | tr 'N-ZA-Mn-za-m' 'A-Za-z' 
```

## Level 13

* Convert the hexdump into binary

```
xxd -r data.txt binary.txt
```

* Determine the file types
* Rename the file to include the extension
* Decompress the archives

```
file binary.txt 

mv binary.txt binary.txt.gz
gunzip binary.txt.gz
```

The file name and `.txt` extension are of no consequence, but the `.gz`, `.bz2` and `.tar` extensions are required by `gunzip`, `bunzip2` and `tar` respectively.

One pass of the procedure is listed above. More are needed to complete the level.

## Level 14

Copy the private key to the client machine.

* Modify file permissions
* Use the private key for public key authentication

```
chmod 400 /path/to/sshkey.private
ssh -p 2220 -i /path/to/sshkey.private bandit14@bandit.labs.overthewire.org
```

## Level 15

Connect and provide the password.

```
cat /etc/bandit_pass/bandit14 

telnet localhost 30000
```

## Level 16

Connect and provide the password.

```
openssl s_client -connect localhost:30001
```

## Level 17

* Scan ports in the range
* Probe for service information to find the SSL ports
* Connect and provide the password

```
nmap -p 31000-32000 localhost

nmap -T5 -sV -p 31046,31518,31691,31790,31960 localhost

openssl s_client -connect localhost:31790
```

## Level 18

```
diff passwords.old passwords.new
```

## Level 19

Issue a command when connecting to find the password.

```
ssh -p 2220 bandit18@bandit.labs.overthewire.org cat readme
```

## Level 20

Files in `/etc/bandit_pass` are owned by their respective user.

```
./bandit20-do cat /etc/bandit_pass/bandit20 
```

## Level 22

The user's `crontab` writes the contents of their password file to a file readable by everyone in `/tmp`.

```
cat /etc/cron.d/cronjob_bandit22

cat /usr/bin/cronjob_bandit22.sh 
```

## Level 23

The user's `crontab` writes the contents of their password file to a file readable by everyone in `/tmp`.

```
cat /etc/cron.d/cronjob_bandit23 

cat /usr/bin/cronjob_bandit23.sh 

echo I am user bandit23 | md5sum | cut -d ' ' -f 1

cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

## Level 24

The `crontab` runs every minute, executes scripts in `/var/spool/bandit24`, then removes them. If the script is owned by `bandit23`, it waits 60 seconds to kill the script.

1. Write this oneliner to a script and make it executable.

```
vi 24.sh
chmod +x 24.sh
```

```
#! /usr/bin/env bash

cat /etc/bandit_pass/bandit24 | tee /tmp/path/bandit24
```

2. Replace `/tmp/path` with whatever was created by `mktemp -d`
3. Copy `24.sh` to `/var/spool/bandit24` and wait for the next minute

## Level 25

```
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

## Level 27

Files in `/etc/bandit_pass` are owned by their respective user.

```
./bandit27-do cat /etc/bandit_pass/bandit27
```

## Level 28

Create a new directory with `mktemp -d` and replace `/tmp/path` with its name.

```
git clone ssh://bandit27-git@localhost/home/bandit27-git/repo /tmp/path

cd /tmp/path
cat README 
```

## Level 29

View changes made to the file.

```
git log -p
```

## Level 30

Switch to a different branch.

```
git branch -a

git log -p
```

## Level 32

Remove `.gitignore` to permit the addition of `key.txt`.

```
cat README.md 

echo 'May I come in?' > key.txt

git rm .gitignore

git add key.txt

git commit

git push
```
