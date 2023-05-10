---
title: SQL Injection - Subdomain tvri.go.id
date: 2021/1/07
description: Write Up
tag: Write Up
author: You
---

![](https://miro.medium.com/max/14000/1*z2ycWiANWQbreVjLBfJYlw.png)

Halo saya Dandy, kali ini saya mau share write up Vulnerability SQL Injection di subdomain website Televisi Republik Indonesia http://tvri.go.id
Sebenarnya BUG ini sudah saya temukan dari tahun 2020, tepatnya di bulan Juni

Penemuan ini bermula dari saya iseng-iseng mengunjungi web http://****.tvri.go.id melalui chrome. tapi saya tertarik pada kolom search yang request method nya adalah [GET]
langsung saja saya membuka cyberfox/mozilla dan membuka http headers guna untuk merekam semua request, dan ini yang saya dapatkan

![](https://miro.medium.com/max/659/0*d1zNDqPY65kZuWZB.jpg)

Yap, menggunakan method [GET] lalu memakai teknik curl di website http://****.tvri.go.id. ok jadi saya langsung mengakses web tersebut, berikut tampilannya

![](https://miro.medium.com/max/2400/0*ukQzYf7AqavyHf4U.jpg)

Menampilkan list judul film/acara yang tayang pada tanggal 24 Juni 2020. lalu saya berpikir untuk memasukkan single quote setelah parameter angka 1, maka seperti ini http://****.tvri.go.id/api/rundown.php?channel=1′. output nya adalah web menjadi blank.

Saya berpikir bahwa ini vulnerability sql injection, sebab vuln sqli bukan hanya “you have an error sql syntax”, tetapi juga di tandai dengan adanya blank atau ada sesuatu yang hilang.

___

Selanjutnya saya melakukan scanning di SQLMap, hasilnya adalah

![](https://miro.medium.com/max/2400/0*LpjSJYH4CVRMMMIs.jpg)

Saya berhasil mendapatkan database nya yaitu rundown. lalu saya ingin mencari user nya, berikut user yang saya dapatkan

![](https://miro.medium.com/max/468/0*j_uy4WQoTBDKPPAl.jpg)

Usernya adalah `web_rundown@localhost`

Saya juga berhasil mendapatkan table dari databasenya

![](https://miro.medium.com/max/2400/0*dUnGBRQ9EQ_aHKv9.jpg)

Beserta informasi sensitif lainnya, seperti username dan password untuk login di web rundown.tvri.go.id

___

Saya berpikir sejenak, “database rundown??, berarti beda website??”. saya berinisiatif bahwa rundown adalah subdomainnya, maka saya mencoba mengakses http://rundown.tvri.go.id, ini dia hasilnya

![](https://miro.medium.com/max/20000/0*Sb7aVeSr7xFMEcW3.jpg)

Benar saja dugaan saya….. itu adalah sebuah subdomain, berarti dapat saya simpulkan database website http://rundown.tvri.go.id berada di ****.tvri.go.id

___

## Timeline Report

* 26 Juni 2020 = mengirim laporan via email bantuan70@bssn.go.id + mengirimkan data diri beserta nomor WhatsApp

* 13 Juli 2020 = IT TVRI Pusat Jakarta menghubungi saya melalui WhatsApp & BUG Di Proses Patch
![](https://media.rafterday.com/files/Greenshot.png)

* 24 September 2020 = BSSN Mengirimkan Sertifikat Apresiasi

Oke mungkin itu saja write up sederhana dari saya, jika ada salah dalam penulisan kata tolong di koreksi ya. terima kasih!

Contact me at [About Me](/about/)