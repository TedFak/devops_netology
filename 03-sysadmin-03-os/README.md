 1. Изменяет текущую директорию. chdir("/tmp")

 2.  openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3

 3.  root@vagrant:~# ping 192.168.0.1 > log &
  
  root@vagrant:~# ps u
 
  root@vagrant:~# rm log
 
  root@vagrant:~# sudo lsof -p 1714
 
  root@vagrant:~# kill 1714
 
 4. Не занимают память, только пустую запись в таблице процессов.

 5. openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3

 openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpthread.so.0", O_RDONLY|O_CLOEXEC) = 3

 openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libdl.so.2", O_RDONLY|O_CLOEXEC) = 3

 openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libexpat.so.1", O_RDONLY|O_CLOEXEC) = 3
 
 6. Выдает основную информацию, доступную в настоящий момент о системе. Part of the utsname information is also accessible via
       /proc/sys/kernel/{ostype, hostname, osrelease, version,
       domainname}.

7. ; по очередно запускает команды. && тоже очердно, только если первая команда завершиться успешно. 

set -e выходит моментально если команда не успешна, если ошибочно завершится одна из команд, разделённых &&, то выхода из шелла не произойдёт.

8. -e Немедленный выход, если команда завершается с ненулевым статусом. 

 -u Рассматривать неустановленные переменные как ошибку при замене. 
 
 -x Печатать команды и их аргументы по мере их выполнения. 
 
 -o pipefail Устанавливает код выхода конвейера на код выхода самой правой команды для выхода с ненулевым статусом или на ноль, если все команды конвейера завершаются успешно.
 
 Завершить безопасно при наличии ошибок и подробный вывод ошибок.
 
 9.  S- ожидает завершения события.

 R- работает

 
