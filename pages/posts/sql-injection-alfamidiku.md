---
title: SQL Injection - alfamidiku.com
date: 2020/6/04
description: Write Up temuan SQL Injection pada alfamidiku.com
tag: Write Up
author: You
---

Halo semuanya, kali ini saya ingin share write up SQL Injection di website alfamidiku.com, pasti kalian semua tau ya dan sering juga dijumpai di pinggir jalan atau dimanapun kalian berada, selengkapnya tentang Alfamidi ada di [Wikipedia](https://id.wikipedia.org/wiki/Alfamidi)

Sebelumnya saya sudah menemukan vulnerable SQLI juga di subdomain website alfamartku.com, langsung aja ya

___

Berikut request headers yang saya dapatkan

![](https://miro.medium.com/max/581/1*5JCyS12vIZt5pOp2HUnqnA.jpeg)

lalu dimana Post Data nya? ini dia post datanya

![](https://miro.medium.com/max/464/1*wXvB-hpcwG6z0oL40BbqMA.jpeg)

Lalu saya mengeceknya di cyberfox dengan menggunakan Hackbar

![](https://miro.medium.com/max/2400/1*cxISaxa7pN_9LFTDnLpg5Q.jpeg)

Ketika saya melakukan inject dengan menggunakan Single Quote pada parameter parent_id respons nya menjadi Blank, saya yakin bahwa vulnerability SQLI

___

Saya mencoba untuk scan di SQLMap dengan command

```
sqlmap -u host.com — data=”.....” --level 3 --risk 3 --dbs --threads 10
```

Hasil dari scannya adalah

![](https://miro.medium.com/max/2400/1*54ct4GD9pEnQxFR-3VAt-g.jpeg)

dan users nya adalah

![](https://miro.medium.com/max/421/1*S6R2mfzS1Nq91N9zfSbVqw.jpeg)

dan ini tablenya, ada 34 table

![](https://miro.medium.com/max/24000/1*-VGKCREDS_UWuRDM96lHWw.jpeg)

Sekian write up sederhana dari saya ini, apabila ada salah dalam penulisan kata mohon dikoreksi, terima kasih sudah berkunjung :D

Artikel ini juga saya post di [Medium](https://medium.com/@dandyrafliansyah) Saya