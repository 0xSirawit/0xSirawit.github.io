---
title: FetchTheFlag CTF 2023-Web-UnhackalbeAndy
date: 2023-10-28 
categories: [Writeups, FetchTheFlag CTF 2023]
tags: [CTF,Web,Github,env,Repo,easy]
---

# Unhackable Andy - Easy
## Description
<sup>Author: @HuskyHacks</sup><br>

Someone might want to let ol' Andy know the old addage - pride goeth before the fall.

Press the Start button on the top-right to begin this challenge.<br>
Connect with:<br>
	`http://challenge.ctf.games:31244`<br>
Please allow up to 30 seconds for the challenge to become available.
## Solution
![[Unhackable1]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Unhackable1.png)There is his GitHub in the website, Let's check it up.
![[Unhackable2]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Unhackable2.png)In `app.py`, The website get username and password from `env`. So we need to find `env` file.
![[Unhackable3]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Unhackable3.png)But there isn't `env` file in GitHub repository. Look carefully at commits history.
![[Unhackable4]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Unhackable4.png)
```
ADMIN_USERNAME=unhackableandy	
ADMIN_PASSWORD=ThisIsASUPERStrongSecuredPasswordAndIAMUNHACKABLEANDYYYYBOIIIII133742069LOLlolLOL	
```
use this credential to login and then run `cat flag.txt` in shell box.
![[Unhackable5]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Unhackable5.png)

> Flag: flag{e81b8885d8a5e8d57bbadeb124cc956b}
{: .prompt-tip}