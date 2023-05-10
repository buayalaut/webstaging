---
title: SQL Injection - kompas.id API [Fixed]
date: 2023/1/13
description: Write Up
tag: Write Up
author: You
---

Untuk BUG yang saya temukan di kompas.id sangat critical, sebab saya mendapatkan 3 temuan yang semuanya termasuk dalam High.
SQL Injection, Parameter Tampering & IDOR (Insecure Direct Object Reference)

Awalnya saya melaporkan ke GM Tech kompas.com (karena masih 1 company), 2 hari kemudian saya dihubungi melalui email oleh Sysadmin TI at kompas.id serta mengucapkan Terima kasih karena telah membantu melaporkan BUG pada sistem layanan kompas.id apalagi pada API nya.

![](https://media.rafterday.com/kompasid/email.jpeg)

Rewards dari temuan ini adalah saya mendapatkan Merchandise dari kompas.id + paket langganan gratis produk digital dari kompas selama 3 Bulan :D
![](https://media.rafterday.com/kompasid/merchandise.jpeg)