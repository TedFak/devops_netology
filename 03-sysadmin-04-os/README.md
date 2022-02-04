
### 1. 
 ##### A. 
  ![А.](https://user-images.githubusercontent.com/95320903/152065804-e0a1a954-7a63-4109-8810-b758244bfcea.png)
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
Лимит открытых дискриптор
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
