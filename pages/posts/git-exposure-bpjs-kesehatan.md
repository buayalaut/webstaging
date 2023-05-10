---
title: SQL Injection - LSP BPJS Kesehatan
date: 2021/3/03
description: Write Up
tag: Write Up
author: You
---

Penemuan ini awalnya bermula dari saya isengiseng mengunjungi web adm-bpjs.lspbnsp.id
![](https://media.rafterday.com/bpjs/Screenshot_5.png)

Vulnerability nya terletak pada direktori .git ketika saya menggunakan dirsearch maka respons nya 200
![](https://media.rafterday.com/bpjs/Screenshot_6.png)

___

Lalu saya mencoba dump direktori .git nya dengan menggunakan GIT Dumper
![](https://media.rafterday.com/bpjs/Screenshot_7.png)

Lalu saya mencoba ekstrak folder dumper nya, dan mendapatkan source code pada web tersebut, beserta informasi sensitif lainnya
![](https://media.rafterday.com/bpjs/Screenshot_8.png)

___

Timeline Report

- Mengirimkan Laporan ke email humas@bpjs-kesehatan.go.id dan hackathonbpjs@bpjs-kesehatan.go.id