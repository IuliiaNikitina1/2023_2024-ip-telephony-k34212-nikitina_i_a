University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [IP-telephony](https://itmo-ict-faculty.github.io/ip-telephony/)

Year: 2023/2024

Group: K34212

Author: Nikitina Iuliia Alekseevna

Lab: Lab1

Date of create: 14.02.2024

Date of finished: 


## Отчет по лабораторной работе №1:
### ["Базовая настройка ip-телефонов в среде Сisco packet tracer"](https://itmo-ict-faculty.github.io/ip-telephony/education/labs2023_2024/lab1/lab1/#1)

#### 1. Цель:
  Изучить рабочую среду Cisco Packet Tracer, ознакомить- ся с интерфейсами основных устройств, типами кабелей, научиться собирать топологию. Изучить построение сети IP-телефонии с помощью маршрутизатора, коммутатора и IP телефонов Cisco 7960 в среде Packet tracer

#### 2. Ход работы:

**Часть 1.**

  В первой части лабораторной работы в среде Cisco Packet Tracer был создан новый проект и собрана схема соединения, состоящая из 7 персональных компьютеров и четырех коммутаторов.
  Полученная схема представлена на рисунке ниже:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%201-1.png" width = "500" height = "300" alt = "scheme-part-1"/>

  Каждому компьютеру был задан IP-адрес и маска:
PC0: 192.168.1.2/24
PC1: 192.168.1.3/24
PC2: 192.168.1.4/24
PC3: 192.168.1.5/24
PC4: 192.168.1.6/24
PC5: 192.168.1.7/24
PC6: 192.168.1.8/24

  Задание IP-адреса и маски компьютеру PC0 представлено на рисунке ниже:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%201-2.png" width = "500" height = "300" alt = "ip-address-for-pc0"/>

  Вслед за добавлением IP-адресов соединение в сети было проверено на практике. Для этого между компьютерами были осуществлены пинги. Результат пинга с PC0 на PC2 представлен на рисунке ниже:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%201-3.png" width = "500" height = "300" alt = "ping-from-pc0-to-pc2"/>

  Результат пинга с PC6 на PC3 представлен на рисунке ниже:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%201-4.png" width = "500" height = "300" alt = "ping-from-pc6-to-pc3"/>

  Оба соединения были установлены успешно.


**Часть 2.**

  Во второй части  работы была собрана новая схема соединения, состоящая из маршрутизатора, коммутатора и двух IP-телефонов:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%202-1.png" width = "500" height = "300" alt = "scheme-part-2"/>

  Имя маршрутизатора Cisco 2811 было изменено на CMERoute, синтаксис ввода слов от DNS серверов был отключен. После этого на маршрутизаторе был настроен интерфейс fa0/0, ему был присвоен адрес 192.168.10.1 с маской 255.255.255.0:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%202-2.png" width = "500" height = "300" alt = "switch-config-1"/>

  Вслед за этим для автоматической настройки IP-телефонов на маршрутизаторе был настроен DHCP сервер: был создан DHCP-пул, которому была задана сеть 192.168.10.0/24. Затем был указан IP-адрес нужного VLAN, соответствующий 192.168.10.1, и включена опция 150, необходимая для того, чтобы IP-телефоны использовали настройки CallManager Express c TFTP сервера. 
  Следующим шагом была выполнена настройка CallManager Express, телефонного сервиса, в автоматическом режиме. Было задано максимальное количество номеров, присваемых IP-телефонам (max-dn 5), максимальное количество IP-телефонов (max-ephones 5), а также IP-адрес голосового шлюза (ip source-address 192.168.10.1 port 2000). После этого было произведено автоматическое назначение внешних номеров. 
  
  Все описанные настройки приведены на рисунке ниже:

  <img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%202-3.png" width = "500" height = "300" alt = "switch-config-2"/>

  Вслед за произведенными конфигурациями на маршрутизаторе, на коммутаторе были выполнены команды, назначающие сети VLAN 1 диапазоны портов fa0/1-fa0/5 и переводящие их в режиме access: 

  <img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%202-4.png" width = "400" height = "300" alt = "router-config"/>

  Наконец, на маршрутизаторе CMERouter были созданы телефонные линии и заданы номера IP-телефонов:

  <img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab1/images/ip%202-5.png" width = "500" height = "300" alt = "switch-config-3"/>

  Результаты проверки исправности работы сети ...

  

#### 3. Вывод:

В ходе лабораторной работы были выполнены все поставленные задачи. ///
