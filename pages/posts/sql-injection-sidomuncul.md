---
title: SQL Injection - Subdomain sidomuncul.co.id
date: 2021/2/26
description: Write Up
tag: Write Up
author: You
---

![](https://media.rafterday.com/sidomuncul/Screenshot_20.png)
Halo, kali ini saya ingin menulis write up SQL Injection di subdomain website sidomuncul.co.id

*Sido Muncul adalah produsen jamu dan obat herbal modern dengan pangsa pasar terbesar di Indonesia. Sido Muncul adalah produsen Tolak Angin*

___

Vulnerability terletak pada page registrasi
![](https://media.rafterday.com/sidomuncul/Screenshot_21.png)

Tepatnya pada kolom provinsi
![](https://media.rafterday.com/sidomuncul/Screenshot_23.png)

Berikut request url yang saya dapatkan setelah mencoba untuk merekam request headers yang berjalan
![](https://media.rafterday.com/sidomuncul/Screenshot_22.png)

___

Berikut database yang saya dapatkan ketika melakukan scan di SQL Map
![](https://media.rafterday.com/sidomuncul/000015.png)

Dan users nya adalah
![](https://media.rafterday.com/sidomuncul/000016.png)

___

Timeline report

- 27 Februari mengirimkan laporan ke email info@sidomuncul.co.id