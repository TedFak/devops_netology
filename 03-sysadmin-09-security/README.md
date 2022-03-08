
### 1.
![image](https://user-images.githubusercontent.com/95320903/157274374-74984a42-acce-4089-8e2a-1b3bf76a7562.png)

### 2.
![image](https://user-images.githubusercontent.com/95320903/157275300-6f1c6aa0-0d10-4b49-9cb3-91cb2620ce6d.png)

### 3.
```BASH
vagrant@vagrant:~$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
Generating a RSA private key
....................+++++
..............+++++
writing new private key to '/etc/ssl/private/apache-selfsigned.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:RU
State or Province Name (full name) [Some-State]:Saratov
Locality Name (eg, city) []:Saratov
Organization Name (eg, company) [Internet Widgits Pty Ltd]:MyOrgan
Organizational Unit Name (eg, section) []:MeOrgan
Common Name (e.g. server FQDN or YOUR name) []:apachetest.com
Email Address []:me@apachetest.com

vagrant@vagrant:~$ sudo cat /etc/apache2/sites-available/apachetest.com.conf
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLHonorCipherOrder On
# Disable preloading HSTS for now.  You can use the commented out header line that includes
# the "preload" directive if you understand the implications.
# Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
# Requires Apache >= 2.4
SSLCompression off
SSLUseStapling on
SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
# Requires Apache >= 2.4.11
SSLSessionTickets Off

vagrant@vagrant:~$ curl 127.0.1.1
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>302 Found</title>
</head><body>
<h1>Found</h1>
<p>The document has moved <a href="https://apachetect.com/">here</a>.</p>
<hr>
<address>Apache/2.4.41 (Ubuntu) Server at 127.0.1.1 Port 80</address>
</body></html>
```
