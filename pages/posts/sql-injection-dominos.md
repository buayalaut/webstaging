---
title: SQL Injection - Subdomain dominos.co.id [Hall of Fame]
date: 2021/2/03
description: Write Up
tag: Write Up
author: You
---

![](https://miro.medium.com/max/24000/1*WfLsELjULT1AthOISw1OKg.png)

Halo, kali ini saya ingin membagikan write up sederhana SQL Injection di [bi.dominos.co.id](https://bi.dominos.co.id) tepatnya pada form login

Reward dari penemuan ini adalah saya mendapatkan Hall Of Fame di [dominos.responsibledisclosure.com](https://dominos.responsibledisclosure.com/hc/en-us/articles/360001378594-Acknowledgments)
(Dandy Rafliansyah)

Penemuan ini awalnya saya iseng-iseng mengunjungi domain utamanya, lalu saya berpikir "mengapa tidak mencari BUG nya saja?" nah awalnya saya mencari BUG di domain utamanya, namun tidak menandakan adanya vulnerability hahaha

Oke next, maka dari itu saya berpikir untuk melakukan scan subdomainnya, dan akhirnya dapatlah subdo bi.dominos.co.id

___

Pada bi.dominos.co.id menampilkan form login, saya berpikir lagi "ah sepertinya tidak vuln", lalu saya mencoba memasukkan single quote pada kolom username dan password guna untuk mengecek apakah vuln atau tidak...

Dan ketika saya klik Sign In maka saya di arahkan/redirect ke dashboard. TAPI, langsung di redirect lagi ke form login. seperti ini gambarannya
![](https://media.rafterday.com/files/dominos1.png)

Lalu ketika saya menambahkan string balance, web tidak redirect ke page dashboard dan menampilkan "Invalid Username & Password"
![](https://media.rafterday.com/files/dominos2.png)

Saya semakin yakin bahwa ini vulnerability terhadap SQL Injection, sebab ketika saya menginjeksikan menggunakan payload balance, tidak error atau tidak redirect

___

Lanjut, saya lalu mencari request URL dan post datanya terlebih dahulu sebelum melakukan scan di SQLMap.
Saya membuka Inspect Element di Chrome lalu ke bagian Network, guna merekam semua request headers web yang sedang saya buka, berikut post media nya
![](https://media.rafterday.com/files/dominos3.png)

___

Lalu saya melakukan scan di SQL Map dengan command

```
sqlmap -u https://bi.dominos.co.id/login/index.php --data="uname=12&psw=12&appUri=/p/7639/" --level=3 --risk=3 --dbs
```

Hasil dari scannya adalah saya mendapatkan 8 database
![](https://media.rafterday.com/files/photo_2021-02-15_23-32-24.jpg)

Dan 14 database Management System User
![](https://media.rafterday.com/files/photo_2021-02-15_23-34-32.jpg)

Beserta informasi sensitif lainnya yang tidak bisa saya Screenshot karena Privacy pihak Domino's

___

Timeline Report

* 03 Februari 2021, Membuat Laporan di [dominos.responsibledisclosure.com](https://dominos.responsibledisclosure.com)

* 05 Februari 2021, BUG Dinyatakan Valid oleh Pihak Domino's Pizza dan dalam proses patch oleh Team terkait

* 08 Februari 2021, Mendapatkan Email dari pihak Domino's Pizza Indonesia bahwa BUG sudah di perbaiki dan mengucapkan Terima Kasih karena sudah Follow Up Vulnerability tersebut
![](https://media.rafterday.com/files/Screenshot_110.png)

* 12 Februari 2021, Pihak Domino's Pusat mengkonfirmasi bahwa Client mereka sudah memperbaiki BUG Tersebut, dan meminta saya untuk Screenshot update BUG bahwa sudah di Patch
![](https://media.rafterday.com/files/Screenshot_111.png)

* 15 Februari 2021, Pihak Domino's Pusat meminta link profile Linkedin atau Twitter guna untuk menambahkan ke halaman Acknowledgements

* (Dandy Rafliansyah) - [Acknowledgements](https://dominos.responsibledisclosure.com/hc/en-us/articles/360001378594-Acknowledgments)
![](https://media.rafterday.com/files/Screenshot_112.png)