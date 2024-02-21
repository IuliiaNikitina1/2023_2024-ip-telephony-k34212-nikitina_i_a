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

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab2/images/ip%201-1.png" width = "500" height = "300" alt = "scheme-part-1"/>

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
ephone 1
 device-security-mode none
 mac-address 00D0.FFA0.8EDE
 type 7960
 button 1:1
!
ephone 2
 device-security-mode none
 mac-address 0060.5C85.AE04
 type 7960
 button 1:2
!
ephone 3
 device-security-mode none
 mac-address 00E0.F783.2720
 type 7960
 button 1:3
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

В результате произведенных настроек IP-телефоны получили следующие IP-адреса и номера телефонов:

IP Phone 0: 192.168.10.4/24 ; 54002
IP Phone 1: 192.168.10.6/24 ; 54001
IP Phone 2: 192.168.10.7/24 ; 54003

Для проверки исправности работы сети был произведен звонок с номера 54002 (IP Phone 0) на номер 54003 (IP Phone 2). На приведенных ниже рисунках видно, что звонок был осуществлен и получен успешно:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab2/images/ip%201-2.png" width = "500" height = "300" alt = "call-1"/>

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab2/images/ip%201-3.png" width = "500" height = "300" alt = "call-2"/>

  **Часть 2.**

Во второй части лабораторной работы была собрана схема, состоящая из одного роутера, одного коммутатора, трех IP телефонов и трех персональных компьютеров. Полученная схема представлена на рисунке ниже:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab2/images/ip%202-1.png" width = "500" height = "300" alt = "scheme-part-2"/>

После составления схемы на коммутаторе был произведен ряд настроек: были созданы вланы 10 (name: Data), 20 (name: Voice) и 99 (name: Management), влану 99 был присвоен IP-адрес и маска, порт fa0/4 был переведен в режим trunk, а порты fa0/1-3 в режим access. 

```
!
interface FastEthernet0/1
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/3
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/4
 switchport trunk native vlan 99
 switchport mode trunk
!
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan99
 ip address 192.168.99.10 255.255.255.0
!
ip default-gateway 192.168.99.1
!
!
```

На коммутаторе для вланов 10, 20 и 99 были созданы логические подынтерфейсы fa0/0.10, fa0/0.20 и fa0/0.99 соответственно. Из DHCP пула были исключены адреса интерфейса маршрутизатора и DNS-сервера. Вслед за этим, для передачи голоса и данных на роутере были настроены DHCP-сервера. 
В конце на устройстве также была произведена настройка телефонного сервиса и заданы номера для всех IP-телефонов в сети: 101, 102 и 103.

```
!
ip dhcp excluded-address 192.168.10.1 192.168.10.9
ip dhcp excluded-address 192.168.20.1 192.168.20.9
!
ip dhcp pool Data
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
ip dhcp pool Voice
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 option 150 ip 192.168.20.1
!
!
!
interface FastEthernet0/0
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
!
interface FastEthernet0/0.99
 encapsulation dot1Q 99 native
 ip address 192.168.99.1 255.255.255.0
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
telephony-service
 max-ephones 3
 max-dn 3
 ip source-address 192.168.20.1 port 2000
!
ephone-dn 1
 number 101
!
ephone-dn 2
 number 102
!
ephone-dn 3
 number 103
!
```

///

#### 3. Вывод:

  ...
