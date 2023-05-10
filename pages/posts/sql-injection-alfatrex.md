---
title: SQL Injection - alfatrex.id
date: 2021/2/10
description: Write Up
tag: Write Up
author: You
---

Halo...

Kali ini saya ingin menulis write up SQLi di website alfatrex.id, sedikit saya jelaskan apa itu Alfatrex?

Alfatrex adalah ekspedisi/jasa pengiriman barang ke seluruh kota di Indonesia, dibawah naungan PT Sumber Alfaria Trijaya Tbk. atau yang biasa kalian sebut Alfamart.
Oke langsung aja ya

___

Penemuan ini awalnya bermula dari saya iseng-iseng mengunjungi web https://alfatrex.id melalui chrome. Lalu saya mencoba register pada web tersebut
![](https://media.rafterday.com/alfatrex/000006.png)

Lalu point inject Vulnerability nya terdapat di kolom kecamatan
![](https://media.rafterday.com/alfatrex/000007.png)

mengapa demikian? karena ketika saya memilih kecamatan A maka di kolom kode pos akan menampilkan data-data kode pos dari kecamatan A.

Selanjutnya saya membuka inspect element > network guna untuk merekam semua request headers dari web yang saya buka. Berikut request url yang saya dapatkan
![](https://media.rafterday.com/alfatrex/000008.png)

Selanjutnya saya melakukan injeksi di parameter kecamatan dengan single quote, maka responsnya code error 500
![](https://media.rafterday.com/alfatrex/000009.png)

Dan ketika menambahkan string balance -- - menampilkan code 200, saya dapat simpulkan ini vulnerability terhadap SQL Injection

___

Selanjutnya saya melakukan scan di SQL Map, dan hasilnya saya mendapatkan 21 database
![](https://media.rafterday.com/alfatrex/000010.png)

Dan 67 users dalam database management systemnya
![](https://media.rafterday.com/alfatrex/000011.png)

___

Timeline Report

- 11 Februari mengirimkan laporan ke email cs@alfadigital.id