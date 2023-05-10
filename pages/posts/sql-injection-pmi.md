---
title: SQL Injection - Subdomain pmi.or.id
date: 2019/6/10
description: Write Up
tag: Write Up
author: You
---

### Halo semuanya...

![Minion](https://cdn-images-1.medium.com/max/1000/1*dSoYR5CQYRpe81ggEmZ1-w.png)

Saya menemukan BUG SQL Injection pada subdomain website Palang Merah Indonesia atau PMI
Yang dimana website tersebut menampilkan data data ****** layanan PMI yang ada di seluruh indonesia. Saya berpikir untuk mencari request URL nya, atau mencari get data nya yang di tampilkan di homepage

Saya mencoba untuk mencari request URL nya menggunakan live http header di mozilla firefox, ini yang saya dapatkan

![ ](https://miro.medium.com/max/1000/1*na9X19JFCs-FMdyA-xLXoA.png)

Respons ketika saya mengakses request urlnya adalah sebagai berikut

![ ](https://miro.medium.com/max/10000/1*tbNm-Mqjd54WQk6VYGh_ZA.png)

Ketika saya membuka request url nya, menampilkan list data data normal. Ketika saya memberikan single quote ( ‘ ) pada angka 2018, respons nya adalah error

![ ](https://miro.medium.com/max/10000/1*isCcpcz3_DUm-ggY0SogFg.png)

## Respons nya adalah

> You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ‘’ )

___

Langkah saya semakin yakin bahwa vulnerable terhadapat SQLI. Selanjutnya saya melakukan scan di sqlmap dengan command

```javascript
sqlmap.py -u “https://*****.pmi.or.id/site/data-nasional?tahun=2018’&semester=0&skema=benef“ --dbs
```

Hasil dari scannya adalah saya mendapatkan 9 Database nya

![ ](https://miro.medium.com/max/5000/1*N9qTyKBd6yAujuu6Q1vyQQ.png)

Beserta informasi sensitif seperti username dan password

![ ](https://miro.medium.com/max/5000/1*7U5dkdAsK7SWqFLDt3Ci5A.png)

___

# Timeline Report

- 10 Juni, 2019 = Mengirimkan laporan ke email info@pmi.or.id & hrd@pmi.or.id (no respons)

- 12 Juni, 2019 = Mendapatkan sebuah pesan dari email developer website pmi.or.id + BUG di patch

![ ](https://miro.medium.com/max/10000/1*5xT5xbHl0k2AKcPpNOGzZw.png)