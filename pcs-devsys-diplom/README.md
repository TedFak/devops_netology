# Курсовая работа по итогам модуля "DevOps и системное администрирование"

Курсовая работа необходима для проверки практических навыков, полученных в ходе прохождения курса "DevOps и системное администрирование".

Мы создадим и настроим виртуальное рабочее место. Позже вы сможете использовать эту систему для выполнения домашних заданий по курсу

## Задание

1. Создайте виртуальную машину Linux.
2. Установите ufw и разрешите к этой машине сессии на порты 22 и 443, при этом трафик на интерфейсе localhost (lo) должен ходить свободно на все порты.
3. Установите hashicorp vault ([инструкция по ссылке](https://learn.hashicorp.com/tutorials/vault/getting-started-install?in=vault/getting-started#install-vault)).
4. Cоздайте центр сертификации по инструкции ([ссылка](https://learn.hashicorp.com/tutorials/vault/pki-engine?in=vault/secrets-management)) и выпустите сертификат для использования его в настройке веб-сервера nginx (срок жизни сертификата - месяц).
5. Установите корневой сертификат созданного центра сертификации в доверенные в хостовой системе.
6. Установите nginx.
7. По инструкции ([ссылка](https://nginx.org/en/docs/http/configuring_https_servers.html)) настройте nginx на https, используя ранее подготовленный сертификат:
  - можно использовать стандартную стартовую страницу nginx для демонстрации работы сервера;
  - можно использовать и другой html файл, сделанный вами;
8. Откройте в браузере на хосте https адрес страницы, которую обслуживает сервер nginx.
9. Создайте скрипт, который будет генерировать новый сертификат в vault:
  - генерируем новый сертификат так, чтобы не переписывать конфиг nginx;
  - перезапускаем nginx для применения нового сертификата.
10. Поместите скрипт в crontab, чтобы сертификат обновлялся какого-то числа каждого месяца в удобное для вас время.

## Результат

Результатом курсовой работы должны быть снимки экрана или текст:

- Процесс установки и настройки ufw
```bash
admin1@admin1:~$ sudo ufw allow 22
Пропуск добавления уже существующего правила
Пропуск добавления уже существующего правила (v6)
admin1@admin1:~$ sudo ufw allow 443
Пропуск добавления уже существующего правила
Пропуск добавления уже существующего правила (v6)
admin1@admin1:~$ sudo ufw allow from 127.0.0.0/8
Пропуск добавления уже существующего правила
admin1@admin1:~$ sudo ufw status
Состояние: активен

В                          Действие    Из
-                          --------    --
22                         ALLOW       Anywhere                  
443                        ALLOW       Anywhere                  
Anywhere                   ALLOW       127.0.0.1                 
Anywhere                   ALLOW       127.0.0.0/8               
22 (v6)                    ALLOW       Anywhere (v6)             
443 (v6)                   ALLOW       Anywhere (v6)             
```
- Процесс установки и выпуска сертификата с помощью hashicorp vault
```bash
admin1@admin1:~$ curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK
admin1@admin1:~$ sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
...                    
Получено 8 610 kB за 19с (463 kB/s)                                                                                    
Чтение списков пакетов… Готово
admin1@admin1:~$ sudo apt-get update && sudo apt-get install vault
...
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 36 пакетов не обновлено.
admin1@admin1:~$ sudo apt install jq
Чтение списков пакетов… Готово
...
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.7) …
root@admin1:/home/admin1# vault server -dev -dev-root-token-id root
==> Vault server configuration:

             Api Address: http://127.0.0.1:8200
                     Cgo: disabled
         Cluster Address: https://127.0.0.1:8201
              Go Version: go1.17.9
              Listener 1: tcp (addr: "127.0.0.1:8200", cluster address: "127.0.0.1:8201", max_request_duration: "1m30s", max_request_size: "33554432", tls: "disabled")
               Log Level: info
                   Mlock: supported: true, enabled: false
           Recovery Mode: false
                 Storage: inmem
                 Version: Vault v1.10.2
...
Development mode should NOT be used in production installations!
admin1@admin1:~$ export VAULT_ADDR=http://127.0.0.1:8200
admin1@admin1:~$ export VAULT_TOKEN=root

```
- Процесс установки и настройки сервера nginx
```bash

```
- Страница сервера nginx в браузере хоста не содержит предупреждений 
```bash

```
- Скрипт генерации нового сертификата работает (сертификат сервера ngnix должен быть "зеленым")
```bash

```
- Crontab работает (выберите число и время так, чтобы показать что crontab запускается и делает что надо)
```bash

```

## Как сдавать курсовую работу

Курсовую работу выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Также вы можете выполнить задание в [Google Docs](https://docs.google.com/document/u/0/?tgif=d) и отправить в личном кабинете на проверку ссылку на ваш документ.
Если необходимо прикрепить дополнительные ссылки, просто добавьте их в свой Google Docs.

Перед тем как выслать ссылку, убедитесь, что ее содержимое не является приватным (открыто на комментирование всем, у кого есть ссылка), иначе преподаватель не сможет проверить работу. 
Ссылка на инструкцию [Как предоставить доступ к файлам и папкам на Google Диске](https://support.google.com/docs/answer/2494822?hl=ru&co=GENIE.Platform%3DDesktop).
