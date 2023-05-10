---
title: SQL Injection - Subdomain indomaret.co.id
date: 2020/1/13
description: Write Up temuan SQL Injection di subdomain indomaret.co.id
tag: Write Up
author: You
---

Sudah lama saya tidak menulis write up lagi yaa haha.
Kali ini saya ingin menjelaskan bagaimana saya bisa menemukan BUG SQL Injection pada Subdomain indomaret.co.id

![ ](https://miro.medium.com/max/2400/1*U4ZiGKG8oFwZ7JUMJ7PURA.png)

Awalnya saya menemukan suatu subdomain Penerimaan Faktur Indomaret. Jenis Vulnerability ini sangat critical, Sebab saya berhasil mendapatkan ratusan ribu data.

Berikut respons yang saya dapatkan ketika memasukkan single quote (‘)

![ ](https://miro.medium.com/max/2400/1*nuiJKMlXl7LS_--u_8NysQ.png)

Selanjutnya saya mengscan nya di jSQL, Dengan menggunakan Post Data yang saya dapatkan serta Request URL nya.

___

Dan ini list database nya

![ ](https://miro.medium.com/max/351/1*E0Yf9WAbGx6z69dVzQgPOw.png)

Dan ini ratusan ribu data datanya, Di salah satu database nya.

![ ](https://miro.medium.com/max/350/1*9ElFI6onQgHSTVCBjFlkCA.png)

Dan ini informasi sensitif seperti username dan password adminnya

![ ](https://miro.medium.com/max/2400/1*YhlxQh-oiijaLr5OI0JH0Q.png)

## Timeline Report

- 27 Oktober 2019 = Send report via email kontak@indomaret.co.id

Sekian write up dari saya ini, Mohon maaf apabila ada salah penulisan kata, jangan lupa untuk di share yaa :D

Contact me at [About](/about/) for About me