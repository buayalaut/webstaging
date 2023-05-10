---
title: SQL Injection - Subdomain pmi.or.id
date: 2021/2/21
description: Write Up
tag: Write Up
author: You
---

![](https://media.rafterday.com/files/logo-pmi.png)

Halo,

Kali ini saya ingin menulis Write Up BUG SQL Injection di [penugasan.pmi.or.id](https://penugasan.pmi.or.id)

BUG ini sudah di Perbaiki oleh Developer website pmi.or.id, setelah saya melaporkannya langsung melalui Whatsapp

___

Penemuan ini awalnya saya iseng-iseng mengunjungi website pmi.or.id, oh ya sebelumnya pada tahun 2019 saya menemukan BUG di pmer.pmi.or.id juga

Oke lanjut, ketika saya melakukan injeksi pada kolom username & password menampilkan `you have an error sql syntax`
![](https://media.rafterday.com/files/Screenshot_124.png)

Berikut request url dan post data yang saya dapatkan
![](https://media.rafterday.com/files/Screenshot_125.png)

Post data
![](https://media.rafterday.com/files/Screenshot_126.png)

Dan saya mencoba menginjeksinya secara manual, dan mendapatkan order by error di 27
![](https://media.rafterday.com/files/Screenshot_127.png)

___

Selanjutnya saya melakukan scan di SQL Map dengan command

```
sqlmap -u http://penugasan.pmi.or.id --data="username=23&password=23" --level=3 --risk=3 --dbs
```

Baru juga mulai scanning, sudah muncul tulisan `connection was forcibly closed by the target url`
![](https://media.rafterday.com/files/Screenshot_128.png)

Saya menambahkan command `--proxy=` agar bisa melanjutkan scanning nya memakai proxy

Berikut hasil dari scanning nya, saya mendapatkan 2 database nya
![](https://media.rafterday.com/files/Screenshot_130.png)

Dan database management system usernya
![](https://media.rafterday.com/files/Screenshot_131.png)

Dan beberapa tables di database nya
![](https://media.rafterday.com/files/photo_2021-02-24_00-12-17.jpg)

Dan beberapa columns di table nya
![](https://media.rafterday.com/files/photo_2021-02-24_00-17-03.jpg)

Beserta informasi sensitif lainnya seperti username & password
![](https://media.rafterday.com/files/photo_2021-02-24_00-19-19.jpg)

___

Timeline Report

- Mengirimkan laporan via Whatsapp Developer PMI Pusat
![](https://media.rafterday.com/files/Screenshot_132.png)

- BUG di Fixed & Meminta izin untuk membuat Write Up
![](https://media.rafterday.com/files/Screenshot_133.png)