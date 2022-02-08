
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


