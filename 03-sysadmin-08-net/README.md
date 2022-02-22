### 1.
```bash
route-views>show ip route 188.232.17.73
Routing entry for 188.232.16.0/22
  Known via "bgp 6447", distance 20, metric 0
  Tag 6939, type external
  Last update from 64.71.137.241 4d18h ago
  Routing Descriptor Blocks:
  * 64.71.137.241, from 64.71.137.241, 4d18h ago
      Route metric is 0, traffic share count is 1
      AS Hops 3
      Route tag 6939
      MPLS label: none
route-views>show bgp 188.232.17.73
BGP routing table entry for 188.232.16.0/22, version 311631013
Paths: (23 available, best #7, table default)
  Not advertised to any peer
  Refresh Epoch 1
  3333 1257 1299 9049 50543
    193.0.0.56 from 193.0.0.56 (193.0.0.56)
      Origin IGP, localpref 100, valid, external
      Community: 1257:50 1257:51 1257:2000 1257:3528 1257:4103
      path 7FE16362A348 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  1351 6939 9049 50543
    132.198.255.253 from 132.198.255.253 (132.198.255.253)
      Origin IGP, localpref 100, valid, external
      path 7FE09A4D6958 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  8283 1299 9049 50543
    94.142.247.3 from 94.142.247.3 (94.142.247.3)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 1299:30000 8283:1 8283:101
      unknown transitive attribute: flag 0xE0 type 0x20 length 0x18
        value 0000 205B 0000 0000 0000 0001 0000 205B
              0000 0005 0000 0001
      path 7FE0B10B3FC0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  852 1299 9049 50543
    154.11.12.212 from 154.11.12.212 (96.1.209.43)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE02A14DBA0 RPKI State not found
      rx pathid: 0, tx pathid: 0
```
### 2.
```bash
root@vagrant:~# echo "dummy" >> /etc/modules
root@vagrant:~# echo "options dummy numdummies=2" > /etc/modprobe.d/dummy.conf
 cat /etc/network/interfaces
...
auto dummy0
iface dummy0 inet static
        address 10.2.2.2/32
        pre-up ip link add dummy0 type dummy
        post-down ip link del dummy0
root@vagrant:~# sudo modprobe -v dummy numdummies=2
insmod /lib/modules/5.4.0-91-generic/kernel/drivers/net/dummy.ko numdummies=2 numdummies=0 numdummies=2
root@vagrant:~# ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
3: eth0.1400@eth0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
4: eth0.10@eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
5: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether 76:76:b2:40:a7:ab brd ff:ff:ff:ff:ff:ff
6: dummy1: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether f2:f8:6a:6f:2f:eb brd ff:ff:ff:ff:ff:ff
root@vagrant:~# ip route add 192.168.2.0/24 dev dummy0
Error: Device for nexthop is not up.
```
### 3.
Локальный адрес - 127.0.0.1 этот сервис доступен только на этом компьтере.
0.0.0.0 или :: означает любой адрес, к таким сервисам могут подключаться из сети.
```bash
vagrant@vagrant:~$ sudo netstat -ntlp | grep LISTEN
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      601/systemd-resolve
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      847/sshd: /usr/sbin
tcp6       0      0 :::22                   :::*                    LISTEN      847/sshd: /usr/sbin
```
### 4.
systemd-resolved — служба systemd, выполняющая разрешение сетевых имён для локальных приложений.
systemd-networkd — системный демон для управления сетевыми настройками.
```bash
vagrant@vagrant:~$ sudo netstat -nulp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
udp        0      0 127.0.0.53:53           0.0.0.0:*                           601/systemd-resolve
udp        0      0 10.0.2.15:68            0.0.0.0:*                           598/systemd-network
```
### 5. 
![Diagram](https://raw.githubusercontent.com/TedFak/devops_netology_2/main/03-sysadmin-08-net/Untitled%20Diagram.drawio.png)
