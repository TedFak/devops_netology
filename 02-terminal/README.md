
1. cd это встроенная оболочка. Cd используюется для перехода в дирикторию и не влияет на рабочий каталог.
2. grep -c <some_string> <some_file> 
3. systemd(1) 

  ![image](https://user-images.githubusercontent.com/95320903/150128448-0e594ed5-eae0-41ea-af4e-2ea152f947a6.png)
  
4. ![image](https://user-images.githubusercontent.com/95320903/150140402-99fdaf2c-015a-4b8e-aea3-2ca3efcb12ed.png)

 ![image](https://user-images.githubusercontent.com/95320903/150140370-4b794906-db4d-4627-9ad0-e4211b462ae9.png)

5. ![image](https://user-images.githubusercontent.com/95320903/150143132-2d33662d-56f4-46a1-9196-e7fd3ea27bd8.png)
6. ![image](https://user-images.githubusercontent.com/95320903/150349316-491b5d71-2bea-464e-82a9-2442fc713431.png)


7. bash 5>&1 Создаст дескриптор 5 и перенапрвет на stdout

 echo netology > /proc/$$/fd/5 отправит stdout на созданный дескриптор 5 
 ![image](https://user-images.githubusercontent.com/95320903/150292903-0183ac34-e04b-413b-8f0f-326feea550c7.png)

8. 
 ![image](https://user-images.githubusercontent.com/95320903/150311152-7022370d-bbf3-444e-b52c-94ecad3f8404.png)

![image](https://user-images.githubusercontent.com/95320903/150311104-2e9c0b09-cfa1-4751-8a21-f6b4d520beef.png)

9. Выведет все переменные окружения с которыми работает процесс. vim proc/5671/environ.
10. /proc/[pid]/cmdline Этот доступный только для чтения файл содержит полную командную строку для процесса, если этот процесс не является зомби.           
/proc/[pid]/exe этот файл представляет собой символическую ссылку, содержащую фактическую путь к выполняемой команде.
11. SSE4 cat /proc/cpuinfo | grep sse 
12. ssh-keygen
 Скопировал ключ в /.ssh/authorized_keys
 
 ![image](https://user-images.githubusercontent.com/95320903/150366945-ec738d03-71cd-4363-841c-c52f1e52bcd9.png)

13. 
14. sudo tee допишет файл и выведет добавленную строку в консоль. А sudo echo выполняется перенаправление оболочкой, у которой нет разрешения на запись.
