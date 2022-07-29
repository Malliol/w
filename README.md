# w

https://www.mgnhost.ru/vds.php

перейдите по ссылке 

и там надо выбрать и купить

![image](https://user-images.githubusercontent.com/90931685/181714756-ae7e14f6-ce21-4147-924c-9b80488167bf.png)

![image](https://user-images.githubusercontent.com/90931685/181714789-f0c54e2b-d5c4-4d9e-bd0f-564e57c44232.png)

и после чего надо пейти на сам сервер 

и там устоновить CenteOS - это ОП 

после чего надо подключиться к самой машине через https://termius.com/ 

и после чего надо выполнить ряд команд 

Обновляем CenteOS
yum update


если CentOS 8 - и ошибка обновления

> sudo sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-*
> sudo sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*

Ставим нужный софт

> yum install -y wget unzip net-tools

Смотрим настойки сети

> ifconfig

Монтируем tempfs в каталог /tmp

> mount -t tmpfs tmpfs /tmp

Загружаем Image файл CHR RouterOS с сайта MikroTik.

> cd /tmp
> wget https://download.mikrotik.com/routeros/7.1.5/chr-7.1.5.img.zip

Распаковываем скачанный образ из архива

> unzip chr-7.1.5.img.zip

Записываем образ на жесткий диск

> dd if=chr-7.1.5.img of=/dev/vda bs=4M oflag=sync

Где vda диск системы, узнать диск можно командой fdisk -l
Принудительная перезагрузка

> echo 1 > /proc/sys/kernel/sysrq
> echo b > /proc/sysrq-trigger

После через сайт нашего хостинга надо зайти в консоль и там проверить установку микро тика 

Устанавливаем настройки интерфейсов, настройки берем из ранее записанных.

> /ip address add interface=ether1 address=XXX.XXX.XXX.XXX/YY

Добавляем маршрут по умолчанию:

> /ip route add dst-address=0.0.0.0/0 gateway=ZZZ.ZZZ.ZZZ.ZZZ/32
