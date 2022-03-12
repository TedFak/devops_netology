
### 1.
![image](https://user-images.githubusercontent.com/95320903/157274374-74984a42-acce-4089-8e2a-1b3bf76a7562.png)

### 2.
![image](https://user-images.githubusercontent.com/95320903/157275300-6f1c6aa0-0d10-4b49-9cb3-91cb2620ce6d.png)

### 3.
```BASH
admin1@admin1-VirtualBox:~$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
Generating a RSA private key
...........................................................................................................................+++++
...............................+++++
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
Common Name (e.g. server FQDN or YOUR name) []:apachetest.lab
Email Address []:host@apachetest.lab
admin1@admin1-VirtualBox:~$ systemctl restart apache2
```
![image](https://user-images.githubusercontent.com/95320903/157947335-7118a4f1-b01b-4a28-96a4-4b3aab0e049c.png)

Не очень понял почему у меня такая ошибка
```bash
мар 11 22:38:24 admin1-VirtualBox apachectl[2629]: AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message
мар 11 22:38:24 admin1-VirtualBox systemd[1]: Started The Apache HTTP Server.
```
### 4.
```bash
vagrant@vagrant:~/TLC/testssl.sh$ ./testssl.sh -U --sneaky https://www.google.com/

###########################################################
    testssl.sh       3.1dev from https://testssl.sh/dev/
    (88cf7e6 2022-03-09 20:16:24 -- )

      This program is free software. Distribution and
             modification under GPLv2 permitted.
      USAGE w/o ANY WARRANTY. USE IT AT YOUR OWN RISK!

       Please file bugs @ https://testssl.sh/bugs/

###########################################################

 Using "OpenSSL 1.0.2-chacha (1.0.2k-dev)" [~183 ciphers]
 on vagrant:./bin/openssl.Linux.x86_64
 (built: "Jan 18 17:12:17 2019", platform: "linux-x86_64")


Testing all IPv4 addresses (port 443): 74.125.205.99 74.125.205.147 74.125.205.106 74.125.205.103 74.125.205.105 74.125.205.104
--------------------------------------------------------------------------------
 Start 2022-03-11 19:54:04        -->> 74.125.205.99:443 (www.google.com) <<--

 Further IP addresses:   74.125.205.104 74.125.205.105 74.125.205.103 74.125.205.106 74.125.205.147
                         2a00:1450:4010:c02::63 2a00:1450:4010:c02::68 2a00:1450:4010:c02::67 2a00:1450:4010:c02::6a
 rDNS (74.125.205.99):   le-in-f99.1e100.net.
 Service detected:       HTTP


 Testing vulnerabilities

 Heartbleed (CVE-2014-0160)                not vulnerable (OK), no heartbeat extension
 CCS (CVE-2014-0224)                       not vulnerable (OK)
 Ticketbleed (CVE-2016-9244), experiment.  not vulnerable (OK)
 ```
### 5.
```bash
admin1@admin1-VirtualBox:~$ ssg-ketgen
admin1@admin1-VirtualBox:~$ ssh-copy-id 10.0.2.15
admin1@admin1-VirtualBox:~$
