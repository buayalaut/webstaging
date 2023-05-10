---
title: Git Exposure AWS S3 Key - Kompas.com [Fixed]
date: 2022/12/15
description: Write Up
tag: Write Up
author: You
---

Halo, pada kali ini saya ingin menulis write up kerentanan git exposure pada apiz.kompas.com
Akibat dari kerentanan ini, saya mendapatkan access key Amazon AWS S3 yang terdapat pada file .env

Sebelumnya saya membaca salah satu berita terkait FS di Kompas.com, awalnya saya tidak pernah terpikirkan untuk melakukan pentest ke Kompas.com karena yang pasti mereka sudah mementingkan arsitektur keamanan pada websitenya. selanjutnya saya menuju ke salah satu berita dan melakukan view-source pada halaman berita tersebut

Saya melihat beberapa request API yang terdapat pada web. Dan sampai pada akhirnya saya menemukan web API yaitu di apiz.kompas.com yang digunakan untuk menarik data video yang ditampilkan pada halaman berita

![](https://media.rafterday.com/kompas/Picture1.png)

Karena saya penasaran web API nya, selanjutnya saya melakukan scanning directory pada web API tersebut dengan menggunakan tools dirsearch. Berikut hasil yang didapatkan

![](https://media.rafterday.com/kompas/Picture2.png)

Dari hasil scanning menggunakan dirsearch, terdapat bahwa pada directory .git respons yang didapat yaitu 200 atau artinya respons sukses. Lalu saya membuka web pada directory tersebut

![](https://media.rafterday.com/kompas/Picture3.png)

403 Forbidden. Ketika respons yang di dapat 403 forbidden berarti pada directory tersebut terdapat directory dan files yang lainnya, saya ragu untuk melakukan scanning menggunakan tools git Dumper, karena saya berpikir pasti terdapat WAF atau max limit request pada website/directory tersebut.

___

Selanjutnya saya iseng mencoba Dump file objects nya dengan tools Git Dumper berharap berhasil, awalnya tetap pesimis :D
Dan hasilnya adalah respons yang didapat yaitu berhasil melakukan Dump directory git nya

![](https://media.rafterday.com/kompas/Picture4.png)

Berikut hasil file objects yang berhasil di Download

![](https://media.rafterday.com/kompas/Picture5.png)

___

Selanjutnya saya melakukan extract file object yang sudah di download tersebut dengan menggunakan git Extractor.
Berikut hasil yang di dapatkan

![](https://media.rafterday.com/kompas/Picture6.png)

Dan saya berhasil melakukan extract nya, struktur directory yang terdapat dalam website dapat terbaca.

Lalu saya mencari informasi sensitif apa yang bisa saya dapat agar temuan saya ini termasuk dalam High/Critical.
Sebenarnya kerentanan git disclosure ini tingkat kerentanan nya Medium, Karena meskipun hanya mendapatkan source code dan struktur directory pada website dapat memungkinkan attacker mengetahui lebih lanjut kerentanan di setiap file dan directory, dan dapat juga mempermudah attacker melakukan upload backdoor jika directory root nya sudah diketahui

Dan saya mendapatkan file database.php pada directory config

![](https://media.rafterday.com/kompas/Picture7.png)

Dan ternyata isinya adalah informasi username & password untuk login ke database. Saya tidak menyangka bahwa saya bisa melakukan pencarian kerentanan di website Kompas.com, meskipun hanya di subdomainnya saja.

___

Selanjutnya saya mencari kerentanan yang lainnya yang critical, yaitu saya mendapakat file .env yang berisikan informasi access key amazon AWS S3 Bucket

Dan saya mencoba melakukan exploitasi dengan access key AWS tersebut, dan hasilnya adalah semua AWS S3 Bucket milik kompas.com bisa di akses dengan menggunakan access key tersebut.

![](https://media.rafterday.com/kompas/s3-kompas.jpeg)

Dengan bisa diaksesnya semua AWS S3 Bucket dengan access key, maka attacker bisa melakukan upload malicious file kedalam bucket tersebut.

___

Setelah saya mencari2 kontak person IT Internal nya dan akhirnya saya mendapatkan kontak Head of IT at Kompas.com yang bernama Bapak Ihwan Santoso, lalu saya melaporkan temuan BUG ini pada tanggal 12 Desember 2022

Lalu di respons pada tanggal 13 Desember 2022 lalu menyampaikan BUG akan segera di perbaiki segera

![](https://media.rafterday.com/kompas/Screenshot_95.png)

Lalu di tanggal 15 Desember pak Ihwan mengirimkan email kembali, dan mengkonfirmasi bahwa BUG sudah dilakukan perbaikan dan mengucapkan terima kasih serta mengirimkan Sertifikat Apresiasi

![](https://media.rafterday.com/kompas/Screenshot_96.png)

Sertifikat Apresiasi dapat dilihat pada halaman [Rewards](https://buayalaut.co/rewards) di website ini

Terima kasih sudah berkunjung dan membaca Write Up sederhana dari saya ini, See u :D