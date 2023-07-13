# Don't Bump Your Head(er)

> Try to bypass my security measure on this site! http://165.227.106.113/header.php

__Category:__ Web [MEDIUM]

## Approach

Berikut ini adalah tampilan pertama kali laman `http://165.227.106.113/header.php` ketika dibuka di browser

![Page screenshot](docs/page.png)

Terdapat pesan
> Sorry, it seems as if your user agent is not correct, in order to access this website. The one you supplied is: xxxxxxxx

Pesan tersebut bermaksud memberitahu pengunjung jika User-Agent yang digunakan ketika request/mengunjungi laman tersebut bukan User-Agent yang cocok.

Selanjutnya, ketika laman di *inspect element*, terdapat comments yang nampak mencurigakan, yaitu
> <!-- Sup3rS3cr3tAg3nt  -->

