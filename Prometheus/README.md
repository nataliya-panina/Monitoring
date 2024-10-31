# Домашнее задание к занятию «Система мониторинга Prometheus»
Это задание для самостоятельной отработки навыков и не предполагает обратной связи от преподавателя. Его выполнение не влияет на завершение модуля. Но мы рекомендуем его выполнить, чтобы закрепить полученные знания.

Цели задания
Научиться устанавливать Prometheus
Научиться устанавливать Node Exporter
Научиться подключать Node Exporter к серверу Prometheus
Научиться устанавливать Grafana и интегрировать с Prometheus
Чеклист готовности к домашнему заданию
 Просмотрите в личном кабинете занятие "Система мониторинга Prometheus"
Инструкция по выполнению домашнего задания
Сделайте fork репозитория c шаблоном решения к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
Выполните клонирование этого репозитория к себе на ПК с помощью команды git clone.
Выполните домашнее задание и заполните у себя локально этот файл README.md:
впишите вверху название занятия и ваши фамилию и имя;
в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
для корректного добавления скриншотов воспользуйтесь инструкцией «Как вставить скриншот в шаблон с решением»;
при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в инструкции по MarkDown.
После завершения работы над домашним заданием сделайте коммит (git commit -m "comment") и отправьте его на Github (git push origin).
В личном кабинете прикрепите ссылку на решение в виде md-файла в вашем Github.
Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.
## Задание 1
Установите Prometheus.

Процесс выполнения
Выполняя задание, сверяйтесь с процессом, отражённым в записи лекции
Создайте пользователя prometheus
Скачайте prometheus и в соответствии с лекцией разместите файлы в целевые директории
Создайте сервис как показано на уроке
Проверьте что prometheus запускается, останавливается, перезапускается и отображает статус с помощью systemctl
Требования к результату
 Прикрепите к файлу README.md скриншот systemctl status prometheus, где будет написано: prometheus.service — Prometheus Service Netology Lesson 9.4 — [Ваши ФИО]

## Решение
1.Создаю пользователя prometheus, скачиваю архив из github, распавовываю его
```
sudo useradd --no-create-home --shell /bin/false prometheus
wget https://github.com/prometheus/prometheus/releases/download/v2.55.0/prometheus-2.55.0.linux-amd64.tar.gz
tar xvfz prometheus-2.55.0.linux-amd64.tar.gz
ll prometheus-2.55.0.linux-amd64.tar.gz
```
2. Создаю каталоги для файлов prometheus
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
Запуск prometheus
```
sudo /usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/var/lib/prometheus/ \
--web.console.templates=/etc/prometheus/consoles/ --web.console.libraries=/etc/prometheus/console_libraries/
```

## Задание 2
Установите Node Exporter.

Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
Скачайте node exporter приведённый в презентации и в соответствии с лекцией разместите файлы в целевые директории
Создайте сервис для как показано на уроке
Проверьте что node exporter запускается, останавливается, перезапускается и отображает статус с помощью systemctl
Требования к результату
 Прикрепите к файлу README.md скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО]
 
## Решение

## Задание 3
Подключите Node Exporter к серверу Prometheus.

Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
Отредактируйте prometheus.yaml, добавив в массив таргетов установленный в задании 2 node exporter
Перезапустите prometheus
Проверьте что он запустился
Требования к результату
 Прикрепите к файлу README.md скриншот конфигурации из интерфейса Prometheus вкладки Status > Configuration
 Прикрепите к файлу README.md скриншот из интерфейса Prometheus вкладки Status > Targets, чтобы было видно минимум два эндпоинта
Дополнительные задания со звёздочкой*
Эти задания дополнительные. Их можно не выполнять. Это не повлияет на зачёт. Вы можете их выполнить, если хотите глубже разобраться в материале.

## Решение

## Задание 4*
Установите Grafana.

Требования к результату
 Прикрепите к файлу README.md скриншот левого нижнего угла интерфейса, чтобы при наведении на иконку пользователя были видны ваши ФИО

## Решение

## Задание 5*
Интегрируйте Grafana и Prometheus.
