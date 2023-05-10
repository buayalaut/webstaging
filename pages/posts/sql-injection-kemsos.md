---
title: SQL Injection - Subdomain kemsos.go.id
date: 2018/3/27
description: Write Up
tag: Write Up
author: You
---

hallo good people!, Kembali lagi bersama saya dandy :D
Kali ini saya akan share BUG yang saya temukan di subdomain kemsos.go.id, Bug tersebut adalah SQL Injection ( Post data ).
Langsung saja ya...

Waktu itu saya sedang menjelajah di website kemsos.go.id, dan saya menemukan suatu subdomain, yang dimana kita harus meng-select menu yang tersedia, nanti output akan muncul di bawah form tersebut

![ ](https://miro.medium.com/max/7000/1*PDB3bfxGLjkrrLMRGC8zdQ.png)

Saya berpikir untuk mencari post data dan request url nya. saya menggunakan inspect element lalu ke network, dan saya berhasil mendapatkan post data dan request url nya

![ ](https://miro.medium.com/max/7000/1*fthIT4lik-DhFJIISKbrXQ.jpeg)

Saya langsung saja membuka request url nya, dan lihat respons dari request url nya adalah

![ ](https://miro.medium.com/max/7000/1*OBZBlJHCmvquonB2P5Pm6Q.png)

Lalu saya juga mendapatkan Post datanya

![ ](https://miro.medium.com/max/579/1*Kyiiw1Cpx7HQ6eYVCZQmVQ.png)

___

Selanjutnya saya melakukan scanning di SQLMap dengan command

```javascript
sqlmap.py -u “url.com” — data=”post datanya” —dbs
```
Hasilnya adalah

![ ](https://miro.medium.com/max/9000/1*yM0Wv9qbEfK0QrlSmdmKKQ.png)

Total ada 64 database yang berhasil saya dapatkan, beserta informasi email, username dan password

![ ](https://miro.medium.com/max/7000/1*SQvOv0tYzWwaOV-rDlqvnA.png)

Dan saya berhasil masuk ke page adminnya

![ ](https://miro.medium.com/max/700/1*LPhnY-HFKUdK63jFYLId2g.png)

Sekian write up sqli sederhana ini, jangan lupa claps nya ya, agar saya semangat untuk meng-share write up sqli lainnya!
