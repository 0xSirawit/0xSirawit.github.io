---
title: FetchTheFlag CTF 2023-Warmup-QuickMaths
date: 2023-10-28 
categories: [Writeups, FetchTheFlag CTF 2023]
tags: [CTF,Warmup,Programming,socket]
---

# Quick Maths
## Description
<sup>Author: @soups71</sup><br>
To try and get better grades in math, I made a program that gave me timed quizzes. Funny thing is that as I got better at the questions in this test, I got worse grades on my math tests.  
  
**NOTE: Float answers are rounded to 1 decimal points.**  
**NOTE: And here's another twist... the answers to division questions depend on _integer division_ or _double division_. I.e.,**  
`3/5 = 0`  
`3/5.0 = .6`  

**Press the `Start` button in the top-right to begin this challenge.**
## Solution
```bash
$ nc challenge.ctf.games 31006

Welcome! To be honest, I am a Computer Science major but I was never any good at math in school. I seemed to always get Cs.  

Note to self: Round all answers to 1 decimal point, where applicable.

Do you want to give it a chance? (Y/n): Y
Awesome, good luck!
What is 68.1 * 69.8? 4753.38
Too Slow!!!
Good bye :(
```
I connect to `challenge.ctf.games`. It responds when I answer `too slow`. That means I need to write the script to answer it. I  use the tool call [pwntools](https://github.com/Gallopsled/pwntools) in python.
```python
from pwn import *
target = remote('challenge.ctf.games',32493)
target.recvuntil("(Y/n):")
target.sendline("y")
count = 0
# answer 100 questions.
for j in range(100): 
    print(target.recvline().decode())
    x = target.recvuntil(b"?").decode().split()
    print(x)
    #Make this conditional because of division problem.
    if '.' not in ''.join(x):
        x[-3] = int(x[-3])
        x[-1] = int(x[-1][:-1])
        if x[-2] == '+':
            target.sendline(str(round(x[-3]+x[-1], 1)))
        if x[-2] == '*':
            target.sendline(str(round(x[-3]*x[-1], 1)))
        if x[-2] == '-':
            target.sendline(str(round(x[-3]-x[-1], 1)))
        if x[-2] == '/':
            print(x[-3],"/",x[-1],str(round(x[-3]//x[-1], 1)))
            target.sendline(str(round(x[-3]//x[-1], 1)))
    else:
        x[-3] = float(x[-3])
        x[-1] = float(x[-1][:-1])
        if x[-2] == '+':
            target.sendline(str(round(x[-3]+x[-1], 1)))
        if x[-2] == '*':
            target.sendline(str(round(x[-3]*x[-1], 1)))
        if x[-2] == '-':
            target.sendline(str(round(x[-3]-x[-1], 1)))
        if x[-2] == '/':
            print(x[-3],"/",x[-1],str(round(x[-3]/x[-1], 1)))
            target.sendline(str(round(x[-3]/x[-1], 1)))
    count +=1
    print(count)
print(target.recvline().decode())
print(target.recvuntil(b"}").decode())
target.interactive()
```

after I ran the script. Got it!
```
Great job, you just answered 100 math problems! You might not fail the next math test. Here is your reward!!!
flag{77ba0346d9565e77344b9fe40ecf1369}
```

> Flag: flag{77ba0346d9565e77344b9fe40ecf1369}
{: .prompt-tip }