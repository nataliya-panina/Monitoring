# Домашнее задание к занятию «Система мониторинга Zabbix. Часть 2» - Panina Nataliya
Цели задания  
- Научитья создавать свои шаблоны в Zabbix, добавлять в Zabbix хосты и связывать шаблон с хостами
- Научиться составлять кастомный дашборд
- Научиться создавать UserParameter на Bash
- Научиться создавать Python-скрип, добавляться в него UserParameter и прикреплять к шаблону
- Научиться создавать Vagrant-скрипты для Zabbix Agent
---
## Задание 1

Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста.
### Процесс выполнения

    Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
    В веб-интерфейсе Zabbix Servera в разделе Templates создайте новый шаблон
    Создайте Item который будет собирать информацию об загрузке CPU в процентах
    Создайте Item который будет собирать информацию об загрузке RAM в процентах

### Требования к результату

    Прикрепите в файл README.md скриншот страницы шаблона с названием «Задание 1»
## Решение
Configuration -> Templates -> Create Template
![Template](https://github.com/nataliya-panina/zabbix1/blob/main/img/Zadanie1.png)
## Задание 2

Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>. Например: ivanovii-1 и ivanovii-2.
### Процесс выполнения

    Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
    Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
    Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
    Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
    Прикрепите за каждым хостом шаблон Linux by Zabbix Agent
    Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

### Требования к результату

    Результат данного задания сдавайте вместе с заданием 3
## Решение

![Hosts](https://github.com/nataliya-panina/zabbix1/blob/main/img/zadanie2.png)

## Задание 3

Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.
### Процесс выполнения

    Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
    Зайдите в настройки каждого хоста и в разделе Templates прикрепите к этому хосту ваш шаблон
    Так же к каждому хосту привяжите шаблон Linux by Zabbix Agent
    Проверьте что в раздел Latest Data начали поступать необходимые данные из вашего шаблона

### Требования к результату

    Прикрепите в файл README.md скриншот страницы хостов, где будут видны привязки шаблонов с названиями «Задание 2-3». Хосты должны иметь зелёный статус подключения
## Решение
![Zadanie 3](https://github.com/nataliya-panina/zabbix1/blob/main/img/Zadanie3.png)

## Задание 4

Создайте свой кастомный дашборд.
### Процесс выполнения

    Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
    В разделе Dashboards создайте новый дашборд
    Разместите на нём несколько графиков на ваше усмотрение.

### Требования к результату

    Прикрепите в файл README.md скриншот дашборда с названием «Задание 4»
## Решение

![Dashboard](https://github.com/nataliya-panina/zabbix1/blob/main/img/Zadanie4.png)

## Задание 5* со звёздочкой

Создайте карту и расположите на ней два своих хоста.
Процесс выполнения

    Настройте между хостами линк.
    Привяжите к линку триггер, связанный с agent.ping одного из хостов, и установите индикатором сработавшего триггера красную пунктирную линию.
    Выключите хост, чей триггер добавлен в линк. Дождитесь срабатывания триггера.

Требования к результату

    Прикрепите в файл README.md скриншот карты, где видно, что триггер сработал, с названием «Задание 5»
## Решение
1. Добавить картинку в библиотеку  
    Administration -> General -> Images -> Type=Background -> Create Background
2. Создание карты:  
    Monitoring -> Maps -> Create map  
    Name, Width, Height, Backgroung image -> Add
3. Добавление хостов:  
    Edit map -> Map element Add/Remove
![AddMapElement](https://github.com/nataliya-panina/zabbix1/blob/main/img/AddMapElement.png)
4. Создание связи между элементами:
![CreateLink](https://github.com/nataliya-panina/zabbix1/blob/main/img/CreateLink.png)
5. При недоступности хоста:
![Zadanie 5](https://github.com/nataliya-panina/zabbix1/blob/main/img/zadanie5.png)    

## Задание 6* со звёздочкой
Создайте UserParameter на bash и прикрепите его к созданному вами ранее шаблону. Он должен вызывать скрипт, который:

    при получении 1 будет возвращать ваши ФИО,
    при получении 2 будет возвращать текущую дату.
Прикрепите в файл README.md код скрипта, а также скриншот Latest data с результатом работы скрипта на bash, чтобы был виден результат работы скрипта при отправке в него 1 и 2
## Решение



## Задание 7* со звёздочкой

Доработайте Python-скрипт из лекции, создайте для него UserParameter и прикрепите его к созданному вами ранее шаблону. Скрипт должен:

    при получении 1 возвращать ваши ФИО,

    при получении 2 возвращать текущую дату,

    делать всё, что делал скрипт из лекции.

    Прикрепите в файл README.md код скрипта в Git. Приложите в Git скриншот Latest data с результатом работы скрипта на Python, чтобы были видны результаты работы скрипта при отправке в него 1, 2, -ping, а также -simple_print.*
### Задание 8* со звёздочкой

Настройте автообнаружение и прикрепление к хостам созданного вами ранее шаблона.
Требования к результату

    Прикрепите в файл README.md скриншот правила обнаружения, а также скриншот страницы Discover, где видны оба хоста.*
## Решение
![Discovery](https://github.com/nataliya-panina/zabbix1/blob/main/img/DiscoveryRules.png) 
![Zadanie 8](https://github.com/nataliya-panina/zabbix1/blob/main/img/Zadanie8.png) 
### Задание 9* со звёздочкой

Доработайте скрипты Vagrant для 2-х агентов, чтобы они были готовы к автообнаружению сервером, а также имели на борту разработанные вами ранее параметры пользователей.

    Приложите в GitHub файлы Vagrantfile и zabbix-agent.sh.*
