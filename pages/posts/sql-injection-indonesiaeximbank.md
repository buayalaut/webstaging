---
title: SQL Injection - Subdomain indonesiaeximbank.go.id
date: 2021/2/11
description: Write Up
tag: Write Up
author: You
---

![](https://www.indonesiaeximbank.go.id/site/uploads/logo/5a1b8dd4394a7-59f6af2772d2b-logo.png)

Halo,
Kali ini saya ingin menulis write up SQLi di subdomain website indonesiaeximbank.go.id, terkait detailnya sebagai berikut
___

Vulnerability ini terletak pada kolom Provinsi, ketika saya select Provinsi DKI Jakarta, maka di kolom Kab/kota menampilkan data-data dari Provinsi DKI Jakarta
![](https://media.rafterday.com/eximbank/Screenshot_4.png)

Berikut request headers yang saya dapatkan ketika saya memilih negara
Indonesia, dan saya mendapatkan Request URL nya yaitu [GET]
![](https://media.rafterday.com/eximbank/Greenshot.png)

Lalu saya mencoba mengakses Request URL tersebut, berikut respons nya
![](https://media.rafterday.com/eximbank/000002.png)

Lalu saya melakukan check single quote pada parameter region_type, dan
respons nya menampilkan `http code, error 500`
![](https://media.rafterday.com/eximbank/000003.png)

Saya berpikir ini vulnerable terhadap SQL Injection, sebab ketika melakukan
input single quote, respons web adalah http error 500.

Tidak semua yang menampilkan error 500 berarti vulnerable SQL Injection,
tetapi kemungkinan bisa terjadi.

___

Selanjutnya saya mencoba melakukan scanning di SQL Map dengan command

```
sqlmap -u "https://********.indonesiaeximbank.go.id/api/regions/search?region_type=DISTRICT*****" --level=3 --risk=3 –dbs
```

Maka hasil scan nya adalah saya mendapatkan 2 database
![](https://media.rafterday.com/eximbank/000004.png)

Dan 2 users nya adalah
![](https://media.rafterday.com/eximbank/000005.png)

___

Timeline report

- 11 Februari 2021 mengirimkan laporan ke BSSN