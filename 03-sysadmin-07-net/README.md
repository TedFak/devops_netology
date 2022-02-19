
### 1.
В LINUX:
```bash
vagrant@vagrant:~$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::a00:27ff:feb1:285d  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:b1:28:5d  txqueuelen 1000  (Ethernet)
        RX packets 174148  bytes 248496925 (248.4 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 32548  bytes 2421106 (2.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 407  bytes 38608 (38.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 407  bytes 38608 (38.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
В WINDOWS:
```
PS C:\Users\User> ipconfig

Настройка протокола IP для Windows


Адаптер Ethernet Ethernet:

   DNS-суффикс подключения . . . . . :
   Локальный IPv6-адрес канала . . . : fe80::24d1:3ec7:6b4:89bf%7
   IPv4-адрес. . . . . . . . . . . . : 192.168.0.110
   Маска подсети . . . . . . . . . . : 255.255.255.0
   Основной шлюз. . . . . . . . . : 192.168.0.1

Адаптер Ethernet VirtualBox Host-Only Network:

   DNS-суффикс подключения . . . . . :
   Локальный IPv6-адрес канала . . . : fe80::11bb:816e:ae9a:9d1c%9
   IPv4-адрес. . . . . . . . . . . . : 192.168.56.1
   Маска подсети . . . . . . . . . . : 255.255.255.0
   Основной шлюз. . . . . . . . . :

Адаптер Ethernet Сетевое подключение Bluetooth:

   Состояние среды. . . . . . . . : Среда передачи недоступна.
   DNS-суффикс подключения . . . . . :
   ```
### 2.
LLDP – протокол для обмена информацией между соседними устройствами.
```bash
root@vagrant:~# lldpctl
-------------------------------------------------------------------------------
LLDP neighbors:
-------------------------------------------------------------------------------
```
### 3.
Используется технология - VLAN.

Используется пакет команд vlan.
```bash
vagrant@vagrant:~$ cat /etc/network/interfaces
auto eth0.10
iface eth0.10 inet static
        address 192.168.1.1
        netmask 255.255.255.0
        vlan_raw_device eth0
```
### 4.
##### Типы агрегации интерфейсов: 
 * mode=0 (balance-rr)
 * mode=1 (active-backup)
 * mode=2 (balance-xor)
 * mode=3 (broadcast)
 * mode=4 (802.3ad)
 * mode=5 (balance-tlb)
 * mode=6 (balance-alb)

##### Опции балансировки:
 * arp_interval
 * arp_ip_target
 * downdelay
 * lacp_rate
 * max_bonds
 * miimon
```bash
vagrant@vagrant:~$ cat /etc/network/interfaces
...
auto bond0

iface bond0 inet static
    address 10.31.1.5
    netmask 255.255.255.0
    network 10.31.1.0
    gateway 10.31.1.254
    bond-slaves eth0 eth1
    bond-mode active-backup
    bond-miimon 100
    bond-downdelay 200
    bond-updelay 200
```
### 5.
В сети с маской /29 8 Ip-адресов.

Из сети с маской /24 можно получить 32 подсети с маской /29.
```bash
vagrant@vagrant:~$ ipcalc -b 10.10.10.0/29
Address:   10.10.10.0
Netmask:   255.255.255.248 = 29
Wildcard:  0.0.0.7
=>
Network:   10.10.10.0/29
HostMin:   10.10.10.1
HostMax:   10.10.10.6
Broadcast: 10.10.10.7
Hosts/Net: 6                     Class A, Private Internet
vagrant@vagrant:~$ ipcalc -b 10.10.10.0/24
Address:   10.10.10.0
Netmask:   255.255.255.0 = 24
Wildcard:  0.0.0.255
=>
Network:   10.10.10.0/24
HostMin:   10.10.10.1
HostMax:   10.10.10.254
Broadcast: 10.10.10.255
Hosts/Net: 254                   Class A, Private Internet
vagrant@vagrant:~$ ipcalc -b 10.10.10.0/24 /29
...
 32.
Network:   10.10.10.248/29
HostMin:   10.10.10.249
HostMax:   10.10.10.254
Broadcast: 10.10.10.255
Hosts/Net: 6                     Class A, Private Internet


Subnets:   32
Hosts:     192
```
### 6.

### 7.
