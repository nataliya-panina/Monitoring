# Домашнее задание к занятию «Система мониторинга Zabbix» Panina Nataliya
## Задание 1

Установите Zabbix Server с веб-интерфейсом.  
## Процесс выполнения

    Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
    Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
    Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

### Требования к результаты  

    Прикрепите в файл README.md скриншот авторизации в админке.
    Приложите в файл README.md текст использованных команд в GitHub.
## Решение
1.  Устанавливаю Postgres
```
sudo apt update  
sudo apt postgresql
```
2.  Устанавливаю репозиторий Zabbix:  
![Zabbix](https://www.zabbix.com/download?zabbix=6.0&os_distribution=debian&os_version=11&components=server_frontend_agent&db=pgsql&ws=apache)  
```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb  
apt update  
```
3. Устанавливаю Zabbix сервер и веб-интерфейс
```
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
```
4. Создаю базу данных:
```
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'
sudo -u postgres createdb -O zabbix zabbix 
```
5. На хосте Zabbix сервера импортирую начальную схему и данные.
```
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```
6. Настройка базы данных для Zabbix сервера
```
nano /etc/zabbix/zabbix_server.conf
DBPassword=123456789
```
7. Запускаю процессы Zabbix сервера и настраиваю его запуск при загрузке ОС, а также убеждаюсь, что они активны.
```
sudo systemctl restart zabbix-server apache2
sudo systemctl enable zabbix-server apache2
sudo systemctl status zabbix-server apache2
```
8. Отврываю браузер, ввожу IP адрес сервера/zabbix
![Zabbix-users](https://github.com/nataliya-panina/zabbix1/blob/main/zabbix-users.png)
## Задание 2  
Установите Zabbix Agent на два хоста.  
## Процесс выполнения

    Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
    Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
    Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
    Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

## Требования к результаты

    Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
    Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
    Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
    Приложите в файл README.md текст использованных команд в GitHub
    
## Решение
На два хоста устанавливаю zabbix-agent и проверяю его активность
```
sudo apt install zabbix-agent
sudo systemctl status zabbix-agent
```
Чтобы дать возможность подключения к серверу, редактирую файл /etc/zabbix/zabbix_agent.conf
```
nano /etc/zabbix/zabbix_agent.conf
Server=127.0.0.1, 10.128.0.0/24
sudo nano restart zabbix_agentd.service
sudo nano status zabbix_agentd.service
```
![Подключение](https://github.com/nataliya-panina/zabbix1/blob/main/server%2Bhost.png)
![Monitiring](https://github.com/nataliya-panina/zabbix1/blob/main/data.png)
![Host](https://github.com/nataliya-panina/zabbix1/blob/main/testhost-log.png)
![Logs](https://github.com/nataliya-panina/zabbix1/blob/main/logs_srv_host.png)
## Задание 3 со звёздочкой*

Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.
## Требования к результаты

    Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:
