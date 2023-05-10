---
title: SQL Injection - Subdomain mncplay.id
date: 2020/10/15
description: Write Up
tag: Write Up
author: You
---

![](https://miro.medium.com/max/700/1*jaBXfnFDeWa8_Z-LgXZZnQ.png)

Halo semuanya
Kali ini saya ingin share write up SQL Injection di payment.mncplay.id, langsung aja yaa

Sebelumnya saya menemukan vulnerability pada billing.mncplay.id, namun tidak lengkap rasanya jika web payment nya tidak ikut. Ketika mengakses payment.mncplay.id tidak ada apa apa, melainkan hanya sebuah tulisan `failed transaction request`

Dan pada akhirnya saya menemukan ID Pelanggan yang belum membayar tagihan MNC Play, dimana saya mendapatkan ID Pelanggan seseorang? saya memanfaatkan fitur search pada Twitter dengan keyword `ID Pelanggan MNC Play`

Berikut ID Pelanggan nya

![](https://miro.medium.com/max/2400/1*oocS6dDppPNc7AEt3mKGTA.png)

Ketika saya mengkonfirmasi dengan klik Ya, saya di arahkan ke web payment.mncplay.id dan menampilkan total tagihan yang harus dibayar

![](https://miro.medium.com/max/2400/1*QS3aK-WAujC_1Eiv6k2wUQ.png)

Ketika saya mengklik salah satu pilihan pembayaran, maka total pembayaran ngereload total harganya. seperti ada sesuatu di balik itu

![](https://miro.medium.com/max/2400/1*W6NwKOF3FUZ7HmaqRCa_hg.png)

Langsung saja saya membuka inspect element lalu ke network, dan merekam semua file dan respons headers pada web tersebut. dan akhirnya saya mendapatkan request url tersebut beserta post data nya

![](https://miro.medium.com/max/2400/1*kBILEhMQ_iH_uQUY-jHyxQ.png)

___

Setelah itu saya melakukan check secara manual menggunakan Hackbar pada mozilla firefox atau cyberfox.

Respons normal

![](https://miro.medium.com/max/2400/1*hzPUv1eSVKuJ4vYLbvPA8w.png)

Response setelah menginjeksi dengan single quote pada parameter `merchant_code`

![](https://miro.medium.com/max/700/1*b2ofbNA1Pv8Z1IP6BinWEQ.png)

Response setelah menambahkan balance `-- -` response nya menampilkan data data normal, namun total harganya berubah

![](https://miro.medium.com/max/641/1*l2f7ghMS3Cb9qjRwnygXBw.png)

___

Hasil scan di SQL Map

![](https://miro.medium.com/max/700/1*t8nzC6byT6_jxKmFud4_oQ.jpeg)

Dan 7 table dari salah satu database

![](https://miro.medium.com/max/2400/1*xEZN-v93J4TPdKUxe6j5UA.jpeg)

Beserta informasi rahasia dan sensitif pelanggan lainnya.

___

## Timeline Report

- 26 September 2020, Mengirimkan laporan ke email ccare.mncplay@mncgroup.com

- 28 September 2020, Mengirimkan laporan ke email bos.mncplaymedia@mncgroup.com

Mungkin cukup sampai disini saja write up sederhana ini, jika ada salah dalam penulisan kata, mohon di koreksi
Jangan lupa di share yaa, agar saya semangat untuk share write up BUG lagi hehe, sampai jumpa!

Contact me at [About me](/about/)