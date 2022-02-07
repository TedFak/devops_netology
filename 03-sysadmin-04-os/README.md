
### 1. 
 ![image](https://user-images.githubusercontent.com/95320903/152739295-9e229287-991d-4d27-a3f8-ab5ddf24a121.png) 

 ##### B. 
 ![B.](https://user-images.githubusercontent.com/95320903/152066251-b1f6f31c-cf4a-4813-8ca0-491c685dae0a.png)
 ##### C.
  ![C.](https://user-images.githubusercontent.com/95320903/152066817-32f2af37-960c-4b4f-abf2-94c859861aab.png)

 ### 2. 
 ##### CPU 
`node_cpu_seconds_total{cpu="0",mode="idle"} 2526.39`

`node_cpu_seconds_total{cpu="0",mode="iowait"} 7.22`

`node_cpu_seconds_total{cpu="0",mode="irq"} 0`

##### MEMORY
`node_memory_MemFree_bytes 1.22032128e+08`

`node_memory_Mlocked_bytes 1.8972672e+07`
##### DISK
`node_disk_writes_merged_total{device="dm-0"} 0`

`node_disk_writes_merged_total{device="sda"} 1559`
##### NETWORK
`node_network_transmit_packets_total{device="eth0"} 4352`

`node_network_transmit_packets_total{device="lo"} 736`

`node_network_transmit_bytes_total{device="eth0"} 733237`

`node_network_transmit_bytes_total{device="lo"} 967884`

### 3. 
 ![image](https://user-images.githubusercontent.com/95320903/152520458-922a56e8-c48d-4cf1-9b04-bf1120d02358.png)

### 4.
Да, dmesg выводит о системы виртуализации
```bash
vagrant@vagrant:~$ dmesg | grep "virtual"
[    0.003258] CPU MTRRs all blank - virtualized system.
[    0.095327] Booting paravirtualized kernel on KVM
[    2.910080] systemd[1]: Detected virtualization oracle.
```
### 5. 
Лимит открытых дескрипторов
```bash
vagrant@vagrant:~$ sysctl fs.nr_open
fs.nr_open = 1048576
```
```Bash
vagrant@vagrant:~$ ulimit -Hn #Жесткий лимит может быть повышен только пользователем root.
1048576
vagrant@vagrant:~$ ulimit -Sn #Мягкий предел может быть изменен процессом в любое время.
1024
``` 
### 6.
```bash 
root@vagrant:~# unshare -p -f --mount-proc sleep 1h

^C
root@vagrant:~# ps u |grep "sleep"
root        3157  0.0  0.0   5476   592 pts/0    S    14:20   0:00 sleep 1h
root        3159  0.0  0.0   6432   736 pts/0    S+   14:21   0:00 grep --color=auto sleep
root@vagrant:~# ps -e |grep "sleep"
   3157 pts/0    00:00:00 sleep
root@vagrant:~# nsenter -t 3157 -p -m -F
root@vagrant:/# ps
    PID TTY          TIME CMD
      1 pts/0    00:00:00 sleep
     12 pts/0    00:00:00 ps
root@vagrant:/#
```
### 7.
`:(){ :|:& };:` -это ворк бомба. Она вызывает саму себя и переводит вывод в фоновый режим.
```bash
vagrant@vagrant:~$ :(){ :|:& };:
[1] 17321
vagrant@vagrant:~$ -bash: fork: retry: Resource temporarily unavailable
-bash: fork: retry: Resource temporarily unavailable
...
vagrant@vagrant:~$ dmesg | grep "fork"
[13728.112456] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-3.scope
vagrant@vagrant:~$ ulimit -S -u 100
vagrant@vagrant:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 3571
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 100
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```
