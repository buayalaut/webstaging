---
title: Parameter Tampering - Pedulilindungi [Fixed]
date: 2023/3/06
description: Write Up
tag: Write Up
author: You
---

Pada tahun 2023 aplikasi Pedulilindungi berubah nama menjadi SATUSEHAT, rasa ingin melakukan Penetration Testing di aplikasi tersebut sangat tinggi hehe.

Saya menggunakan 2 tools saja, yaitu burpsuite dan android emulator

![](https://media.rafterday.com/kemkes/app.png)

Lalu saya menuju ke bagian vaksin dan imunisasi dan membuka burpsuite, guna untuk intercept request di setiap HTTP Request

Selanjutnya saya menuju ke tiket vaksin dan melakukan intercept request dengan menggunakan Burpsuite

![](https://media.rafterday.com/kemkes/app2.png)

Selanjutnya saya melakukan intercept request pada saat klik pada button Kirim ke Email.

Berikut hasil intercept http request di Burpsuite

![](https://media.rafterday.com/kemkes/Picture4.png)

Lalu saya melakukan resend request yang berhasil di intercept tadi, dan saya mendapatkan email informasi tiket vaksin saya

![](https://media.rafterday.com/kemkes/Picture5.png)

Dan saya melakukan perubahan pada POST Data nya di semua parameternya menjadi seperti ini

> {"nama_lengkap":"KEMENTERIAN KESEHATAN RI","vaksin_ke":"4","program_vaksin":"Kementerian Kesehatan RI","nomor_tiket":"RU-666"}

Berikut respons yang di dapat ketika dilakukan resend request di Burpsuite

![](https://media.rafterday.com/kemkes/Picture6.png)

Dan saya melihat di email, bahwa saya berhasil merubah Value pada parameter tersebut

![](https://media.rafterday.com/kemkes/Picture7.png)

Selanjutnya saya merubah alamat email saya menjadi alamat email lain, dan merubah juga di display name nya. Responsnya berhasil

![](https://media.rafterday.com/kemkes/Picture8.png)

___

Kesimpulan

Penemuan BUG Parameter Tampering level severity nya sangat tinggi, sebab attacker dapat dengan mudah mengubah value pada parameter tersebut, dan digunakan untuk memanipulasi korban

Referensi [https://owasp.org/www-community/attacks/Web_Parameter_Tampering](https://owasp.org/www-community/attacks/Web_Parameter_Tampering)

___

Vulnerability sudah dilaporkan ke tim CSIRT Kementerian Kesehatan RI, dan sudah dilakukan perbaikan.

## Timeline Report

- 06 Maret 2023, 9:00 AM

Mengirimkan report ke email csirt@kemkes.go.id

- 06 Maret 2023, 9:37 AM

Mendapatkan balasan dari email bahwa kerentanan valid dan sedang diproses perbaiki oleh tim

- 08 Maret 2023, 9:25 AM

Dikabarkan melalui email bahwa e-Sertifikat Apresiasi sedang di proses

- 11 April 2023, 11:45 AM

e-Sertifikat Apresiasi dikirimkan ke email

![](https://media.rafterday.com/kemkes/sertif.jpg)

e-Sertifikat valid dan sudah ditandatangani secara elektronik

![](https://media.rafterday.com/kemkes/validation.png)