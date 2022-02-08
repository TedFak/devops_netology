
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

