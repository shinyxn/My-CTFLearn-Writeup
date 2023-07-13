# Don't Bump Your Head(er)

> Try to bypass my security measure on this site! http://165.227.106.113/header.php

__Category:__ Web [MEDIUM]

## Approach

Berikut ini adalah tampilan pertama kali laman `http://165.227.106.113/header.php` ketika dibuka di browser

![first approach](docs/page_screenshot.png)

Terdapat pesan
> Sorry, it seems as if your user agent is not correct, in order to access this website. The one you supplied is: xxxxxxxx

Pesan tersebut bermaksud memberitahu pengunjung jika User-Agent yang digunakan ketika request/mengunjungi laman tersebut bukan User-Agent yang cocok.

Selanjutnya, ketika laman di *inspect element*, terdapat comments yang nampak mencurigakan, yaitu
> `<!-- Sup3rS3cr3tAg3nt  -->`

![comments](docs/comments.png)

Kita berasumsi bahwa `Sup3rS3cr3tAg3nt` merupakan User-Agent yang diminta dalam kasus tersebut, selanjutnya kita perlu memodifikasi [Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) yaitu User-Agent. 

Untuk dapat melakukan hal ini, kita dapat menggunakan Burpsuite, CURL, atau mengirimkan ulang request pada tab network devtools pada Firefox. (opsi lain dengan membuat program sederhana menggunakan bahasa apapun untuk melakukan HTTP request dengan custom header).

Pada case ini kita akan menggunakan CURL

![curl-1](docs/curl-1.png)

Untuk mengirim header menggunakan CURL kita dapat menambahkan `-H` atau `--header` diikuti dengan `"custom_header: custom_header_value"`.

Kita jalankan perintah
> curl http://165.227.106.113/header.php -H "User-Agent: Sup3rS3cr3tAg3nt"

![curl-2](docs/curl-2.png)

Selanjutnya terdapat response
> Sorry, it seems as if you did not just come from the site, "awesomesauce.com".

Isi dari pesan tersebut adalah, referer request tidak berasal dari `awesomesauce.com`. Kita perlu menambahkan referer pada custom header, apa itu [Referer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)?

> The `Referer` header allows a server to identify referring pages that people are visiting from or where requested resources are being used. This data can be used for analytics, logging, optimized caching, and more.
> 
> Source: `https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer`

Terakhir, kita eksekusi menggunakan perintah
> curl http://165.227.106.113/header.php -H "User-Agent: Sup3rS3cr3tAg3nt" -H "Referer: awesomesauce.com"

![curl-3](docs/curl-3.png)

Kita berhasil mendapatkan flagnya
__flag{did_this_m3ss_with_y0ur_h34d}__