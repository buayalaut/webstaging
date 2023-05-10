---
title: SQL Injection - Subdomain gramedia.com
date: 2020/7/28
description: Write Up temuan SQL Injection pada salah satu subdomain gramedia.com
tag: Write Up
author: You
---

Halo semuanya, Kali ini saya ingin share write up SQL Injection di subdomain gramedia.com, tepatnya berada di bukusekolah.gramedia.com

Penemuan ini awalnya bermula dari saya iseng - iseng melakukan recon subdomain dan mendapatkan sub bukusekolah.gramedia.com
lalu saya ke page register
![](https://media.rafterday.com/files/Screenshot_90.png)

Ketika saya ingin melakukan register, saya tertarik pada kolom select Provinsi. karena ketika saya memilih provinsi A maka di kolom Kabupaten/Kota menampilkan data-data yang sesuai dengan di kolom A, seperti ini
![](https://media.rafterday.com/files/Screenshot_91.png)

Lalu saya membuka menu Network pada Inspect Element guna merekam semua request headers yang sedang saya buka, dan saya sudah mendapatkan request url dan post data nya
![](https://media.rafterday.com/files/Screenshot_92.png)

___

Selanjutnya saya melakukan cek di hackbar pada mozilla/cyberfox, maka respons nya adalah
![](https://media.rafterday.com/files/Screenshot_93.png)

Lalu saya coba cek dengan menambahkan single quote pada parameter provinsi=, respons nya media-media yang sebelumnya hilang
![](https://media.rafterday.com/files/Screenshot_94.png)

Lalu saya coba menambahkan string balance -- -, guna memeriksa lebih lanjut apakah vulnerable terhadap SQLi atau tidak, respons nya adalah sama seperti tadi menambahkan single quote.

Lalu karena saya pantang menyerah, maka saya mencoba merubah single quote menjadi double quote. maka respons webnya adalah menjadi blank page, Damn!
![](https://media.rafterday.com/files/Screenshot_97.png)

dan setelah itu saya mencoba menambahkan string balance lagi, ternyata responsnya menampilkan media - media normal
![](https://media.rafterday.com/files/Screenshot_98.png)

Nah disini saya bisa menyimpulkan bahwa ini vulnerable terhadap SQLi (tidak semua vuln, tetapi kemungkinan iya)

___

Selanjutnya saya mencoba melakukan scanning di SQLMap, dan hasilnya adalah saya mendapatkan 8 database dari website tersebut
![](https://media.rafterday.com/files/Screenshot_95.png)

Dan saya juga mendapatkan 6 Users dari website tersebut
![](https://media.rafterday.com/files/Screenshot_96.png)

___

Timeline Report

* 12 Oktober 2020 Mengirimkan laporan ke email customercare@gramedia.com = Mendapat balasan lalu disuruh mengirimkan laporan ke email cs@gramediaprinting.com

* 12 Oktober 2020 Mengirimkan laporan ke email cs@gramediaprinting.com = No respons

* 26 Januari 2021 Mengirimkan laporan ke email cs@gramediaprinting.com untuk kedua kalinya, tetap tidak ada respons