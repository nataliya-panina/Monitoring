# Домашнее задание к занятию «Система мониторинга Prometheus»
Это задание для самостоятельной отработки навыков и не предполагает обратной связи от преподавателя. Его выполнение не влияет на завершение модуля. Но мы рекомендуем его выполнить, чтобы закрепить полученные знания.

Цели задания:
- Научиться устанавливать Prometheus
- Научиться устанавливать Node Exporter
- Научиться подключать Node Exporter к серверу Prometheus
- Научиться устанавливать Grafana и интегрировать с Prometheus

## Задание 1
Установите Prometheus.

### Процесс выполнения
Выполняя задание, сверяйтесь с процессом, отражённым в записи лекции
- Создайте пользователя prometheus
- Скачайте prometheus и в соответствии с лекцией разместите файлы в целевые директории
- Создайте сервис как показано на уроке
- Проверьте что prometheus запускается, останавливается, перезапускается и отображает статус с помощью systemctl
### Требования к результату
 Прикрепите к файлу README.md скриншот systemctl status prometheus, где будет написано: prometheus.service — Prometheus Service Netology Lesson 9.4 — [Ваши ФИО]

## Решение
1.Создаю пользователя prometheus, скачиваю архив из github, распавовываю его
```
sudo useradd --no-create-home --shell /bin/false prometheus
wget https://github.com/prometheus/prometheus/releases/download/v2.55.0/prometheus-2.55.0.linux-amd64.tar.gz
tar xvfz prometheus-2.55.0.linux-amd64.tar.gz
ll prometheus-2.55.0.linux-amd64.tar.gz
```
2. Создаю каталоги для файлов prometheus и копирую в них файлы конфигурации:
```
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo mv prometheus promtool /usr/local/bin
sudo cp -R ./console_libraries /etc/prometheus
sudo cp -R ./consoles /etc/prometheus
sudo mv ./prometheus.yml /etc/prometheus
sudo chown prometheus:prometheus /etc/prometheus /var/lib/prometheus
sudo chown prometheus:prometheus /usr/local/bin/prometheus /usr/local/bin/promtool
```
3. Проверяю работоспособность prometheus
```
sudo /usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/var/lib/prometheus/ \
--web.console.templates=/etc/prometheus/consoles/ --web.console.libraries=/etc/prometheus/console_libraries/
```
В браузере открываю <IP_address>:9090
![image](https://github.com/user-attachments/assets/9c85cdfe-08e8-4222-bb9a-41f08cfcaa2b)

4. Создаю файл сервиса prometheus по пути /etc/systemd/system/prometheus.service
```
[Unit]
Description=Prometheus Service Netology Lesson 9.4 Panina Nataliya
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml \
--storage.tsdb.path=/var/lib/prometheus/ --web.console.templates=/etc/prometheus/consoles/ \
--web.console.libraries=/etc/prometheus/console_libraries/
ExecReload=/bin/kill -HUP $MAINPID Restart=on-failure
[Install]
WantedBy=multi-user.target
```
После этого осталось только запустить prometheus как сервис:
```
sudo systemctl start prometheus
sudo systemctl status prometheus
```
Здесь может возникнуть проблема с правами доступа к каталогу /var/lib/prometheus, так как при старте prometheus создаются файлы с владельцем root, чтобы её устранить, нужно поменять владельца папки на prometheus:prometheus

```
sudo chown prometheus:prometheus /var/lib/prometheus/*
```
![image](https://github.com/user-attachments/assets/332a23f4-e580-470c-8fcd-97dd6d3c3d45)
---
## Задание 2
Установите Node Exporter.

### Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
- Скачайте node exporter приведённый в презентации и в соответствии с лекцией разместите файлы в целевые директории
- Создайте сервис для как показано на уроке
- Проверьте что node exporter запускается, останавливается, перезапускается и отображает статус с помощью systemctl
### Требования к результату
 Прикрепите к файлу README.md скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО]
 
## Решение

## Задание 3
Подключите Node Exporter к серверу Prometheus.

### Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
- Отредактируйте prometheus.yaml, добавив в массив таргетов установленный в задании 2 node exporter
- Перезапустите prometheus
- Проверьте что он запустился
### Требования к результату
 - Прикрепите к файлу README.md скриншот конфигурации из интерфейса Prometheus вкладки Status > Configuration
 - Прикрепите к файлу README.md скриншот из интерфейса Prometheus вкладки Status > Targets, чтобы было видно минимум два эндпоинта
# Дополнительные задания со звёздочкой*
Эти задания дополнительные. Их можно не выполнять. Это не повлияет на зачёт. Вы можете их выполнить, если хотите глубже разобраться в материале.

## Задание 4*
Установите Grafana.

### Требования к результату
 Прикрепите к файлу README.md скриншот левого нижнего угла интерфейса, чтобы при наведении на иконку пользователя были видны ваши ФИО

## Решение

## Задание 5*
Интегрируйте Grafana и Prometheus.

## Решение
