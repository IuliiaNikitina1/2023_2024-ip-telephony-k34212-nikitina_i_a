University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [IP-telephony](https://itmo-ict-faculty.github.io/ip-telephony/)

Year: 2023/2024

Group: K34212

Author: Nikitina Iuliia Alekseevna

Lab: Lab2

Date of create: 16.02.2024

Date of finished: 


## Отчет по лабораторной работе №2:
### ["Конфигурация voip в среде Сisco packet tracer"](https://itmo-ict-faculty.github.io/ip-telephony/education/labs2023_2024/lab2/lab2/)

#### 1. Цель:
   Изучить построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.

#### 2. Ход работы:

**Часть 1.**

В первой части лабораторной работы была собрана схема, состоящая из следующих устройств: одного маршрутизатора Cisco 2811, одного коммутатора Cisco Catalyst 3560 и трех IP телефонов Cisco 7960. Полученная схема представлена на рисунке ниже:

...

После составления схемы на маршрутизаторе был произведен ряд настроек: его название было изменено на CMERouter, синтаксис ввода слов от DNS серверов был отключен. Затем были заданы пароли для защиты маршрутизатора в режиме консоли и в удаленном режиме, после чего был настроен интерфейс fa0/0. Для автоматической настройки компьютеров и IP-телефонов в сети на маршрутизаторе был также настроен DHCP сервер.
Следом за проделанными действиями была произведена настройка CallManager Express, телефонного сервиса в автоматическом режиме. Было задано максимальное количество номеров, присваиваемых IP-телефонам и максимальное количество самих телефонов, а также указан адрес голосового шлюза. Для возможности дальнейшего общения для каждого устройства были созданы телефонные линии и заданы номера. 
Полный список команд, написанных при настройке маршрутизатора, приведен ниже:

```
hostname CMERouter
!
!
!
!
!
ip dhcp pool VOICE
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 option 150 ip 192.168.10.1
!
!
!
no ip domain-lookup
!
!
interface FastEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
!
!
telephony-service
 max-ephones 5
 max-dn 5
 ip source-address 192.168.10.1 port 2000
 auto assign 4 to 6
 auto assign 1 to 5
!
ephone-dn 1
 number 54001
!
ephone-dn 2
 number 54002
!
ephone-dn 3
 number 54003
!
ephone-dn 4
 number 54004
!
ephone-dn 5
 number 54005
!
line con 0
 password cisco
 logging synchronous
 login
!
line aux 0
!
line vty 0 4
 password cisco
 logging synchronous
 login
!
!
!
end
```

Вслед за настройкой маршрутизатора была произведена настройка коммутатора Switch A. Его порты fa0/1-5 были переведены в режим access.

```
!
interface FastEthernet0/1
 switchport mode access
 switchport nonegotiate
 switchport voice vlan 1
!
interface FastEthernet0/2
 switchport mode access
 switchport nonegotiate
 switchport voice vlan 1
!
interface FastEthernet0/3
 switchport mode access
 switchport nonegotiate
 switchport voice vlan 1
!
interface FastEthernet0/4
 switchport mode access
 switchport nonegotiate
 switchport voice vlan 1
!
interface FastEthernet0/5
 switchport mode access
 switchport nonegotiate
 switchport voice vlan 1
!
```

///

  **Часть 2.**

  ...


#### 3. Вывод:

  ...
