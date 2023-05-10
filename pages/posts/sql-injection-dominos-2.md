---
title: SQL Injection - Domino's Pizza [Hall of Fame 2x]
date: 2022/12/15
description: Write Up
tag: Write Up
author: You
---

![](https://miro.medium.com/max/24000/1*WfLsELjULT1AthOISw1OKg.png)

Halo, kali ini saya ingin membagikan write up SQL Injection di [migrationdev.dominos.id](https://migrationdev.dominos.id)

Reward dari penemuan ini adalah saya mendapatkan Hall Of Fame di [dominos.responsibledisclosure.com](https://dominos.responsibledisclosure.com/hc/en-us/articles/360001378594-Acknowledgments)
(Dandy Rafliansyah)

![](https://media.rafterday.com/dominosid/Screenshot_55.png)
___

Sebelumnya saya sudah mendapatkan Hall of Fame pada tahun 2021, artikel write up dapat dilihat di [https://buayalaut.co/blog/sql-injection-dominos/](https://buayalaut.co/blog/sql-injection-dominos/)

Saya mendapatkan domain dominos.id melalui email, selanjutnya saya buka domain dominos.id nya dan ternyata tidak bisa diakses, lalu saya melakukan cek di whois dan ingin melihat mengarah kemana nameserver dari domain dominos.id.

![](https://media.rafterday.com/dominosid/Screenshot_56.png)
___

lalu saya melakukan scanning subdomain dengan menggunakan tools dnscan

![](https://media.rafterday.com/dominosid/Screenshot_57.png)

Dan mendapatkan subdomain [migrationdev.dominos.id](https://migrationdev.dominos.id), selanjutnya saya melakukan intercept pada webnya, dan saya mendapatkan request URL dengan method GET yaitu di
[https://migrationdev.dominos.id/infdominos/ajax/setcrustimage?crust_pizza=24](https://migrationdev.dominos.id/infdominos/ajax/setcrustimage?crust_pizza=24)
___

Selanjutnya saya melakukan scanning di sqlmap dengan command

```
sqlmap.py -u "https://migrationdev.dominos.id/infdominos/ajax/setcrustimage?crust_pizza=24" --level=3 --risk=3 --dbs --threads 10

```

Hasil dari scanning di sqlmap adalah saya berhasil mendapatkan 1 database dominos

![](https://media.rafterday.com/dominosid/Screenshot_42.png)

___

## Timeline Report

* 06 Desember membuat laporan di dominos.responsibledisclosure.com

![](https://media.rafterday.com/dominosid/Screenshot_58.png)

* 08 Desember temuan dinyatakan valid, dan dalam proses diteruskan ke pihak Domino's Pizza Indonesia

![](https://media.rafterday.com/dominosid/Screenshot_59.png)

* 14 Desember temuan sudah diperbaiki, dan disuruh untuk melakukan cek lagi apakah sudah diperbaiki atau belum

![](https://media.rafterday.com/dominosid/Screenshot_60.png)

* 15 Desember meminta informasi Nama Lengkap dan Linkedin atau Twitter untuk dimasukkan ke list Hall of Fame

![](https://media.rafterday.com/dominosid/Screenshot_61.png)

* Hall of Fame diberikan beberapa jam kemudian - Dandy Rafliansyah at [https://dominos.responsibledisclosure.com/hc/en-us/articles/360001378594](https://dominos.responsibledisclosure.com/hc/en-us/articles/360001378594)

![](https://media.rafterday.com/dominosid/Screenshot_62.png)