---
title: FetchTheFlag CTF 2023-Web-BackTheHawks
date: 2023-10-28 
categories: [Writeups, FetchTheFlag CTF 2023]
tags: [CTF,Web,easy]
---

# Back The Hawks - Easy
## Description
<Sup>Author: @HuskyHacks</sup><br>
We are Back the Hawks! We're a non-profit that seeks to protect hawks across the world. We have a vibrant community of Backers who are all passionate about Backing the Hawks! We'd love for you to join us... if you can figure out how to get an access code.  
  
NOTE - any resemblence to other companies, non-profits, services, login portal challenges, and/or the like, living or dead, is completely coincidental.  
  
**Press the `Start` button on the top-right to begin this challenge.**<br>
**Connect with:** <br>
	`http://challenge.ctf.games:31441`
## Solution
![[Hawks]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Hawks.png)I need to find Access Code to register. Hint: The JavaScript of this page is doing something interesting. Let's check it.
![[Hawks1]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Hawks1.png)In `backTheHawksInviteCodes.min.js` There is a function `makeInviteCode()`. Let's call this function.
![[Hawks2]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Hawks2.png)It tells me to send request to `/back/the/hawks/invite/code` with POST method.
```
$ curl -X POST http://challenge.ctf.games:31441/back/the/hawks/invite/code
{"hint":"this message is encrypted, there's no way to break it! Forget about backing the hawks. Your journey ends here.","message":"TB_LRQ_EBOB_YXZHFK_QEB_EXTHP_2023"}
```
`TB_LRQ_EBOB_YXZHFK_QEB_EXTHP_2023` I use https://cryptii.com/pipes/caesar-cipher to decoder the invite code.
![[Hawks3]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Hawks3.png)Invite Code: `WE_OUT_HERE_BACKIN_THE_HAWKS_2023`
after I submit `WE_OUT_HERE_BACKIN_THE_HAWKS_2023` as invite code to register. Got the flag!
![[Hawks4]](https://raw.githubusercontent.com/0xSirawit/Fetch-the-Flag-CTF-2023/main/assets/images/Hawks4.png)

>Flag: flag{3ef532159716ecfb9117f56f4ead4fb6}
{: .prompt-tip}