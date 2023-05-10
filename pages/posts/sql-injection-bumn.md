---
title: SQL Injection - Subdomain bumn.go.id
date: 2020/10/02
description: Write Up
tag: Write Up
author: You
---

Halo, kali ini saya ingin membagikan write up bug SQL Injection di Subdomain bumn.go.id, langsung aja ya
___

Seperti biasa saya melakukan scan Subdomain di website [api.hackertarget.com](https://api.hackertarget.com)
![](https://media.rafterday.com/files/bumn/photo_2021-02-25_16-58-28.jpg)

## Point Inject

Point inject berada di kolom Provinsi, Kab/kota
![](https://media.rafterday.com/files/bumn/bumn1.png)

Berikut request URL dan Post data nya
![](https://media.rafterday.com/files/bumn/bumn2.png)

Respons request url nya
![](https://media.rafterday.com/files/bumn/bumn3.png)

___

Hasil scan di SQL Map
![](https://media.rafterday.com/files/bumn/bumn4.png)

Berikut database management system usernya
![](https://media.rafterday.com/files/bumn/bumn5.png)

___

## Timeline Report

- 02 Oktober 2020 = Mengirimkan laporan ke bantuan70@bssn.go.id

- 11 Februari 2021 = Mengirimkan laporan ke kbumn.ri@bumn.go.id (No respons)