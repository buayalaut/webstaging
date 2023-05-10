---
title: SQL Injection - Subdomain kompas.com [Fixed]
date: 2023/1/04
description: Write Up
tag: Write Up
author: You
---

![](https://media.rafterday.com/kompas2/logokompas.png)

Halo...

Setelah mendapatkan sertifikat apresiasi dari kompas.com karena telah melaporkan vulnerability git disclosure, saya melaporkan lagi temuan SQL Injection di salah satu subdomain kompas.com hehe

Saya mendapatkan sebuah request yang telah saya intercept menggunakan burpsuite, berikut request nya
![](https://media.rafterday.com/kompas2/1.png)

Berikut respons nya ketika saya melakukan resend request
![](https://media.rafterday.com/kompas2/2.png)

Selanjutnya saya melakukan injeksi dengan menggunakan single quote pada parameter Field
Berikut responsnya
![](https://media.rafterday.com/kompas2/3.jpeg)

Respons menunjukkan 500 Internal Server, saya beranggapan bahwa ini vulnerable terhadap SQL Injection. mengapa? karena ketika saya menginjeksi di parameter lain, responsnya bukan 500 Internal Server Error.

___

Untuk mempersingkat waktu, karena ada kerjaan yang harus kerjakan di tempat bekerja saya, maka dari itu saya melakukan scanning di Sqlmap

Berikut hasil scanning di Sqlmap
![](https://media.rafterday.com/kompas2/4.png)

Mendapatkan 163 Database hehe.
Maaf itu adalah log hasil scanning di sqlmap. kalau melakukan scanning lagi tidak bisa, karena BUG sudah di perbaiki :D

___

*   Melaporkan ke General Manager Tech at Kompas.com pada tanggal 03 Januari 2023
*   Mendapatkan balasan email di tanggal 04 Januari 2023, dan BUG di patch di hari itu juga. wahh sangat cepat sekali ya hehe :D
*   Mendapatkan Sertifikat Apresiasi dari GM Tech at kompas.com
![](https://media.rafterday.com/kompas/sertifikat.jpg)