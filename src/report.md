# Операционные системы UNIX/Linux (Базовый).
## Part 1. Установка ОС

![версия ubuntu](images/ubuntu_ver.png)

Проверяем версию Ubuntu после установки

(Команда: cat /etc/issue)

## Part 2. Создание пользователя

Добовляем пользователя testuser и добавляем его в группу adm

- "sudo useradd testuser -d /home/testuser -m -G adm -s /bin/bash"

Проверяем добавление:

- "cat /etc/passwd"

![cat](images/past2_cat.png)

- "groups testuser"

![groups](images/groups_testuser.png)

## Part 3. Настройка сети ОС
### Past 3.1-3.2

Зададим название машины вида user-1

- "sudo hostnamectl set-hostname user-1"

Проверим название машины

- "hostnamectl"

![hostname](images/hostnamectl.png)

Установим время соответсвующее местному времени

- "sudo timedatectl set-timezone Europe/Moscow"

Проверим время

- "timedatectl"

![timedatectl](images/timedatectl.png)

### Past 3.3 Выводим названия сетевых интерфейсов

Выводим названия сетевых интерфейсов при помощи комады

- "ip link show"

![lo](images/lo.png)

<b>Loopback Interface(lo)<b>

Loopback Interface, обозначаемый как lo, — это специальный виртуальный сетевой интерфейс в системе, который используется для внутренних коммуникаций внутри самого компьютера.

Зачем он нужен:

- Внутреннее тестирование: Разработчики могут использовать его для тестирования сетевых программ без необходимости физической сетевой карты или подключения к сети.

- Локальные сервисы: Многие программы и службы, работающие на компьютере, общаются через Loopback Interface. Например, веб-сервер, работающий на вашем компьютере, может обслуживать запросы на 127.0.0.1 (localhost).

- Диагностика: Помогает проверить работу сетевых стэков и программ, не взаимодействуя с внешними сетями.

Как он работает:

- IP-адрес: Loopback Interface обычно использует IP-адрес 127.0.0.1, который также известен как localhost.

- Маршрутизация: Любой трафик, отправленный на 127.0.0.1, не покидает компьютер и сразу же возвращается обратно, как будто он путешествовал через сеть.

### Past 3.4 Получаем ip адрес устройства, на котором мы работаем, от DHCP сервера

Команда:

- "ip addr show"

![ipaddrshow](images/ip_addr_show.png)

<b>DHCP (Dynamic Host Configuration Protocol)<b> — это сетевой протокол, который позволяет устройствам автоматически получать настройки сети, такие как IP-адрес, маска подсети, шлюз по умолчанию и DNS-серверы. Основная цель DHCP — упростить и автоматизировать управление IP-адресами в сети.



### Past 3.5 Ip-адреса


<b>Внутренний IP-адрес шлюза (IP-адрес по умолчанию)<b>

Команда:

- "ip route | grep default | awk '{print $3}"

![iproute](images/ip_route.png)

<b>Внешний IP-адрес шлюза<b>

Команда:

- "curl ifconfig.me"

![ifconfig](images/ifconfig.png)

### Past 3.6 Задали статичные настройки ip, gw, dns

Открываем файл:

- "sudo nano /etc/netplan/00-installer-config.yaml"

И редактируем

![nano](images/nano.png)

Команда для принятия изменений 

- "sudo netplan apply"

- "sudo reboot"

### Past 3.7 Проверили внешний и локальный ip шлюза(значения сошлись)

![reboot](images/reboot.png)

Успешно пропинговали 1.1.1.1 и ya.ru без потерь

![1.1.1](images/ping_ya.ru.png)

## Part 4. Обновление ОС

![upgrade](images/upgrade.png)
![upgrade](images/upgrad.png)

## Past 5 Использование команды sudo

Sudo – это утилита для операционных систем семейства Linux, позволяющая пользователю запускать программы с привилегиями другой учётной записи, как правило, суперпользователя.

![su](images/sudo_test.png)

- "sudo usermod -aG sudo testuser" добавление в группу sudo

- "sudo hostnamectl set-hostname user-2"

![rename](images/rename.png)

## Part 6 Установка и настройка службы времени

Эти команды запустят службу и включат ее для автоматического запуска при каждом старте системы.

- "sudo apt install systemd-timesyncd"

- "sudo systemctl start systemd-timesyncd" AND

- "sudo systemctl enable systemd-timesyncd"

Убедитесь, что служба работает без ошибок:

- "sudo systemctl status systemd-timesyncd"

![time](images/time.png)

![time](images/time2.png)

## Past 7 Установка и использование текстовых редакторов

### Past 7.1 Создание файлов

<b>VIM<b>

- vim test_VIM.txt

![vim](images/vim.png)

VIM Для сохранения и выхода нажал ESC и прописал :w :q

<b>NANO<b>

- nano test_NANO.txt

![nano00](images/nano00.png)

NANO Для сохранения нажал ^X далее Yes и название файла

<b>JOE<b>

- joe test_JOE.txt

![joe](images/joe.png)

JOE Для сохранения и выхода нажал ^KX

### Past 7.2 Изменение файлов без сохранения

<b>VIM<b>

![vim1](images/vim01.png)

VIM Для выхода без сохранения ESC -> :q! -> ENTER

<b>NANO<b>

![nano01](images/nano01.png)

NANO Для выхода без сохранения ^X -> N

<b>JOE<b>

![joe01](images/joe01.png)

JOE Для выхода без сохранения ^C -> y

### Past 7.3 Поиск и замена

<b>VIM<b>

![vim2](images/vim02.png)

VIM Для поиска: /что_ищем

![vim3](images/vim03.png)

VIM Для замены: :s/что_заменить/чем

**NANO**

![nano02](images/nano02.png)

NANO Для поиска: ^W -> что ищем -> ENTER

![nano03](images/nano03.png)

NANO Для замены: ^\ -> что заменить -> чем -> Y

**JOE**

![joe02](images/joe02.png)

JOE Для поиска: ^K F -> что ищем -> I

![joe03](images/joe03.png)

JOE Для замены: ^K F -> что заменить -> R -> чем -> Y

## Past 8 Установка и базовая настройка сервиса SSHD

![ssh00](images/ssh00.png)

- sudo systemctl enable ssh - запуск системы ssh
- sudo nano /etc/ssh/sshd_config - Port 2022
- sudo systemctl restart sshd

![ssh01](images/ssh01.png)

- Отображение процесса ps - выводит сведения о процессах в статическом виде -е - выбор всех процессов | grep sshd - поиск через pipe как вывод грепа для ввода ps

- "sudo reboot"

- netstat -tan

![ssh02](images/ssh02.png)

-tan:

- t - отабражает TCP подключения

- a - Показать состояние всех сокетов; обычно сокеты, используемые серверными процессами не показываются

- n - Показать сетевые адреса как числа. netstat обычно показывает адреса как символы

| Атрибут       | Описание                |
| ------------- |:------------------|
| Proto     | Содержит тип протокола    |
| Recv-Q     | Счетчик байтов не скопированных программой пользователя их этого сокета |
| Send-Q  | Счетчик байтов, не подтвержденных удалленым узлом         |
| Local address  | Адрес и номер порта локального конца сокета        |
| Foreign address  | Адрес и номер порта удаленного конца сокета        |
| State  | Состояние сокета        |

LISTEN - Сокет ожидает входящих подклчений<br>
SYN_SENT - Сокет находящийся в режиме активной попытки установки подключения<br>
0.0.0.0 - это немаршрутизируемый адрес IPv4, который используется в качестве адреса по умолчанию или адреса-заполнителя

## Part 9. Установка и использование утилит top, htop

![top](images/top.png)

<b>Вывод команды top:<b>

- Uptime: 5 минут
- Пользователей: 1
- Загрузка системы: 0,00, 0,02, 0,00
- Процессы: 104 (1 запущенный, 103 в ожидании)
- Загрузка CPU: 0,0% пользовательского времени, 0,0% системного времени, 100% простаивание
- Память: 3920,0 MiB всего, 3469,3 MiB свободно, 150.3 MiB использовано

<b>Использование команды htop<b>

fn + F6-открыть сортировкe

 - отсортированному по PID

![htop](images/htop.png)

- отсортированному по PERCENT_CPU

![htop01](images/htop01.png)

- отсортированному по PERCENT_MEM

![htop02](images/htop02.png)

- отсортированному по TIME

![htop03](images/htop03.png)

fn + F4 для фильтрации

- отфильтрованному для процесса sshd 

![htop04](images/htop04.png)

fn + F3 для поиска

- с процессом syslog, найденным, используя поиск

![htop05](images/htop05.png)

fn + F2 

- с добавленным выводом hostname, clock и uptime<br>

![htop06](images/htop06.png)

## Part 10. Использование утилиты fdisk

- Название: /dev/sda
- Размер: 10 ГБ (гигабайт), что равно 10737418240 байтам.
- Количество секторов: 20971520. 

Разделы:
- /dev/sda1:
Размер: 1 МБ (мегабайт)
Начальный сектор: 2048, Конечный сектор: 4095.
- /dev/sda2:
Размер: 1,8 ГБ (гигабайт)
Начальный сектор: 4096, Конечный сектор: 3674111.
- /dev/sda3:
Размер: 8,3 ГБ (гигабайт)
Начальный сектор: 3674112, Конечный сектор: 20969471.

![fdisk](images/disk.png)
![swap](images/swap.png)

## Past 11 Использование утилиты df

Из вывода команды df для корневого раздела (/) следующая информация:

- Размер раздела: 8,408,452 килобайт
- Размер занятого пространства: 2,2748,976 килобайт
- Размер свободного пространства: 5,210,760 килобайт
- Процент использования: 35%.
- Единица измерения в выводе - килобайты (1K-blocks).
![df00](images/df.png)

Для корневого раздела (/) из df -Th следующие данные:

- Размер раздела: 8,1G
- Размер занятого пространства: 2,7G
- Размер свободного пространства: 5,0G
- Процент использования: 35%
- Тип файловой системы: exp4
![df01](images/df_Th.png)


## Part 12. Использование утилиты du

- ``du``

![du00](images/du.png)

- ``du /home -h``

![du02](images/gu_home_h.png)

- ``du /var -h``

![du03](images/du_var_h.png)

- ``sudo du /var/log -h``

![du04](images/sudo_du_log.png)

- ``sudo du /var/log/* -h``

![du05](images/sudo_du_lg.png)

## Part 13. Установка и использование утилиты ncdu

- ``ncdu ``

![ncdu](images/ncdu.png)


- ``ncdu /home``

![ncdu01](images/ncdu.png)

- ``ncdu /var``

![ncdu02](images/ncdu_var.png)

- ``ncdu /var/log``

![ncdu03](images/ncdu_varlog.png)

## Part 14 Работа с системными журналами

**Последняя авторизация**

![last](images/solo.png)

**Перезапуск OpenSSH Server**

![ressh](images/ressh.png)

![ressh00](images/catsys.png)

## Part 15. Использование планировщика заданий CRON

- ``crontab -e``

![cronrab](images/crontab.png)

- ``grep CRON /var/log/syslog``

![cron](images/CRON.png)

- ``crontab -l``

![cron01](images/cron01.png)

Удаление задач:
- ``crontab -r``
- ``crontab -l``

![cron02](images/cron02.png)