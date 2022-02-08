
### 2.
Жесткая ссылка и файл, для которой она создавалась имеют одинаковые inode. Поэтому жесткая ссылка имеет те же права доступа, владельца и время последней модификации, что и целевой файл.

### 4.
![image](https://user-images.githubusercontent.com/95320903/153000794-e809f6e7-ede4-4f88-b550-44a2dc04a4a3.png)

### 5.
![image](https://user-images.githubusercontent.com/95320903/153004436-6f0478ae-69ec-431a-9956-fdcac1dea4e7.png)

![image](https://user-images.githubusercontent.com/95320903/153005489-9ccc629a-1564-48c2-932d-b7d4d7fcf35e.png)

### 6.
```bash
root@vagrant:~# mdadm --create --verbose /dev/md1 --level=1 -n 2 /dev/sd{b1,c1}
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
mdadm: size set to 2094080K
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md1 started.
```
### 7.
```bash
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
root@vagrant:~# lsblk
...
sdb                         8:16   0  2.5G  0 disk
├─sdb1                      8:17   0    2G  0 part
│ └─md1                     9:1    0    2G  0 raid1
└─sdb2                      8:18   0  511M  0 part
  └─md0                     9:0    0 1018M  0 raid0
sdc                         8:32   0  2.5G  0 disk
├─sdc1                      8:33   0    2G  0 part
│ └─md1                     9:1    0    2G  0 raid1
└─sdc2                      8:34   0  511M  0 part
  └─md0                     9:0    0 1018M  0 raid0
```
### 8.
```bash 
root@vagrant:~# pvcreate /dev/md0 /dev/md1
  Physical volume "/dev/md0" successfully created.
  Physical volume "/dev/md1" successfully created.
  ```
  ### 9.
  ```bash
root@vagrant:~# vgcreate vg /dev/md0 /dev/md1
  Volume group "vg" successfully created
  root@vagrant:~# vgs
  VG        #PV #LV #SN Attr   VSize   VFree
  ubuntu-vg   1   1   0 wz--n- <63.00g <31.50g
  vg          2   0   0 wz--n-  <2.99g  <2.99g
  ```
  ### 10.
  ```bash
  root@vagrant:~# lvcreate -L 100M vg /dev/md0
  Logical volume "lvol0" created.
root@vagrant:~# lvs
  LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  ubuntu-lv ubuntu-vg -wi-ao----  31.50g
  lvol0     vg        -wi-a----- 100.00m
  ```
 ### 11.
 ```bash
 root@vagrant:~# mkfs.ext4 /dev/vg/lvol0
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```
### 12.
```bash
mkdir /tmp/new
mount /dev/vg/lvol0 /tmp/new
```
### 14.
![image](https://user-images.githubusercontent.com/95320903/153075252-42183b25-3485-4f90-81e5-a8358fe0869d.png)
### 15.
```bash
root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0
```
### 16.
```bash 
root@vagrant:~# pvmove /dev/md0 /dev/md1
  /dev/md0: Moved: 12.00%

  /dev/md0: Moved: 100.00%
  ```
  ### 17.
  ```bash
  root@vagrant:~# mdadm -D /dev/md1
/dev/md1:
           Version : 1.2
     Creation Time : Tue Feb  8 14:34:16 2022
        Raid Level : raid1
        Array Size : 2094080 (2045.00 MiB 2144.34 MB)
     Used Dev Size : 2094080 (2045.00 MiB 2144.34 MB)
      Raid Devices : 2
     Total Devices : 2
       Persistence : Superblock is persistent

       Update Time : Tue Feb  8 21:09:55 2022
             State : clean, degraded
    Active Devices : 1
   Working Devices : 1
    Failed Devices : 1
     Spare Devices : 0

Consistency Policy : resync

              Name : vagrant:1  (local to host vagrant)
              UUID : 85a3e676:9c8477f6:cff1d34c:eb708867
            Events : 19

    Number   Major   Minor   RaidDevice State
       -       0        0        0      removed
       1       8       33        1      active sync   /dev/sdc1

       0       8       17        -      faulty   /dev/sdb1
```
### 18.
```bash
root@vagrant:~# dmesg
[27701.361746] md/raid1:md1: Disk failure on sdb1, disabling device.
               md/raid1:md1: Operation continuing on 1 devices.
```
### 19.
```bash
root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0
```
