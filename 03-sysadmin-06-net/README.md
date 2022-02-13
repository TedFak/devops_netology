### 1.
301 Moved Permanently cообщающий клиенту, что страница, перемещена по новому адресу указаном в Location:.. и старый адрес считается устаревшим.
```bash
vagrant@vagrant:~$ telnet stackoverflow.com 80
Trying 151.101.193.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: 16a962ac-ece6-42c7-8b20-3343e727aa19
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Sun, 13 Feb 2022 15:54:12 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-hel1410023-HEL
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1644767653.566074,VS0,VE112
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=fa5bfcec-cda7-1d75-e0b4-6a18c1ccc335; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
### 2.
