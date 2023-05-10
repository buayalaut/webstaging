---
title: SQL Injection - Subdomain alfamartku.com
date: 2020/4/26
description: Write Up temuan SQL Injection pada salah satu subdomain alfamartku.com
tag: Write Up
author: You
---

![ ](https://miro.medium.com/max/2400/1*wSc1Y15rXis5ct8_hf3Q6A.jpeg)

Halo semuanya,
Kali ini saya ingin menulis Write up sederhana yang sesuai dengan judul, saya akan menjelaskan dari awal.
Sebelumnya saya mencari vulnerability di sekitar homepage https://tenant.alfamartku.com/ tapi tidak ada, hanya ada form search, itu juga search nya mengarah ke domain utama.

Karena hanya ada button daftar, maka saya coba klik button tersebut. dan di arahkan ke kolom pengisian identitas

![ ](https://miro.medium.com/max/2400/1*Ocxkhko0DFUZDgqDnsXx7g.png)

Karena form tersebut ada button “next”, berarti pendaftaran tidak hanya sampai disitu saja, masih ada step selanjutnya. maka dengan itu saya membuka inspect element > network, guna merekam semua file dan request url yang sedang saya buka.

___

Di step kedua, saya mendapatkan request headers dari kolom provinsi. yang di kolom tersebut ketika memilih provinsi DKI Jakarta, maka di kolom kab/kota menampilkan data — data dari provinsi DKI.

![ ](https://miro.medium.com/max/2400/1*uI0IOkaFzB9yCWEz9ij2Gg.png)

Dan ini request headers nya

![ ](https://miro.medium.com/max/2400/1*bmV6wOZew5y7a2QGztNy2w.png)

Setelah saya cek, ternyata tidak vulnerable SQLI, oke lanjut

Sampai di step 3, saya mendapatkan request yang dimana ketika menginjeksi single quote pada parameter jns_usaha, tulisan “AIR BERSIH, AIR ISI ULANG” berubah.

![ ](https://miro.medium.com/max/2400/1*yu29w6oYz-3zkNuLU6dI3Q.png)

berikut request headers nya

![ ](https://miro.medium.com/max/2400/1*YPfA-48yV4DqPI4kMGUVpQ.png)

___

Respons normal tanpa memasukan single quote, masih ada tulisan 'air bersih, air isi ulang'

![ ](https://miro.medium.com/max/2400/1*aX6rj_3IXP0sxDKzYBRGrg.png)

Ketika melakukan injeksi dengan single quote, tulisan isi ulang menjadi hilang atau berubah

![ ](https://miro.medium.com/max/2400/1*LeMJglzvV5mDLFzN1XMKfQ.png)

Dan ketika menambahkan balance setelah single quote, maka kembali menampilkan data normal

![ ](https://miro.medium.com/max/2400/1*pKJjo5BJpgPHx5B1erCabg.png)

___

Selanjutnya saya scan di SQL Map, dan ini dia databasenya

![ ](https://miro.medium.com/max/2400/1*Na9NMDovIR4rNzv3XMuQDQ.png)

Dan usersnya adalah

![ ](https://miro.medium.com/max/2400/1*VivT2-07nX8w-cE14mCsOw.png)

## Timeline Report

- 19 Juli 2020, Send report to email sahabat_alfamart@sat.co.id

- 25 Juli 2020, Send report to email corsec@sat.co.id

Mungkin sampai disini saja Write up sederhana dari saya, mohon maaf apabila ada salah dalam penulisan kata.
Jangan lupa untuk di share yaa, agar saya semangat untuk menulis write up kembali. see you!

Contact me at page [About me](/about/)