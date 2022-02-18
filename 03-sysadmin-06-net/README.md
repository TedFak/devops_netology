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

Status Code: 307 Internal Redirect
PING: 279ms Дольше всего обрабатывался запрос Collect.
![image](https://user-images.githubusercontent.com/95320903/153766287-70182981-38dd-4470-91a7-1f5825c66846.png)

### 3. 


### 4.
```bash
whois 188.232.**.**
...
route:          188.232.16.0/22
origin:         AS50543
org:            ORG-CHSB1-RIPE
descr:          CJSC "ER-Telecom Holding" Saratov branch
...
```
### 5.
```bash 
sudo traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  10.0.2.2 [*]  0.563 ms  0.540 ms  0.526 ms
 2  * * *
 ...
 30  * * *
 ```
 ### 6.
 Патеря пакетов на AS15169  172.253.66.116
 ```bash 
                                                                               Packets               Pings
 Host                                                                        Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. AS???    10.0.2.2                                                         0.0%    17    0.4   0.9   0.3   7.4   1.7
 2. AS???    192.168.0.1                                                      0.0%    17    0.8   1.8   0.8  12.7   2.8
 3. AS50543  188.232.3.252                                                    0.0%    16   13.1   2.8   1.2  13.1   2.9
 4. AS50543  109.195.24.18                                                    0.0%    16    2.9   2.5   1.4   4.1   0.8
 5. AS15169  72.14.215.165                                                    0.0%    16   31.9  33.2  31.4  40.0   2.3
 6. AS15169  72.14.215.166                                                    0.0%    16   23.6  25.2  22.6  35.4   3.8
 7. AS15169  142.251.53.69                                                    0.0%    16   18.2  17.9  16.8  26.1   2.2
 8. AS15169  108.170.250.99                                                   6.2%    16   17.6  26.4  17.5  75.7  17.4
 9. AS15169  172.253.66.116                                                  12.5%    16   33.5  35.6  32.6  64.3   8.3
10. AS15169  209.85.254.6                                                     0.0%    16   33.3  35.2  32.4  66.3   8.3
11. AS15169  142.250.56.219                                                   0.0%    16   34.8  34.5  32.6  41.4   2.1
```
### 7.
```bash
dig +trace @8.8.8.8 dns.google
dns.google.             10800   IN      NS      ns1.zdns.google.
dns.google.             10800   IN      NS      ns3.zdns.google.
dns.google.             10800   IN      NS      ns2.zdns.google.
dns.google.             10800   IN      NS      ns4.zdns.google.
```
### 8.
```bash
dig -x 8.8.8.8
...
;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   7069    IN      PTR     dns.google.
...
```
