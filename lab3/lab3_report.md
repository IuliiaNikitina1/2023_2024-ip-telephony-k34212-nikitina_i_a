University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [IP-telephony](https://itmo-ict-faculty.github.io/ip-telephony/)

Year: 2023/2024

Group: K34212

Author: Nikitina Iuliia Alekseevna

Lab: Lab3

Date of create: 29.02.2024

Date of finished: 


## Отчет по лабораторной работе №3:
### ["Использование Asterisk в качестве SIP proxy"](https://itmo-ict-faculty.github.io/ip-telephony/education/labs2023_2024/lab3/lab3/)

#### 1. Цель:
Изучить программный комплекс Asterisk. Настройка Asterisk для локальных звонков.

#### 2. Ход работы:

В начале выполнения работы программный комплекс Asterisk был установлен через терминал.

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/1.png" width = "800" height = "300" alt = "install-asterisk"/>

Затем в файлы /etc/asterisk/sip.conf и /etc/asterisk/extensions.conf были внесены изменения, необходимые для создания двух sip-аккаунтов. 
В /etc/asterisk/sip.conf было добавлено следующее:

```
[1001]
type=friend
host=dynamic
secret=111
context=ext_1001

[1002]
type=friend
host=dynamic
secret=222
context=ext_1002

[internal_calls]
exten => 1001,1,Dial(SIP/1002)
exten => 1002,1,Dial(SIP/1001)

[default]
include => internal_calls
```

А в файл /etc/asterisk/extensions.conf следующее:

```
[ext_1001]
exten => _XXXX,1,Dial(SIP/${EXTEN})

[ext_1002]
exten => _XXXX,1,Dial(SIP/${EXTEN})
```

Asterisk был перезагружен. После перезагрузки все внесенные изменения были успешно применены:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/2.png" width = "500" height = "300" alt = "install-asterisk"/>

С помощью команды ```sudo asterisk -rv``` удалось проверить наличие добавленных аккаунтов. Действительно, аккаунты 1001 и 1002 были успешно созданы и выводятся в списке доступных: 

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/3.png" width = "800" height = "300" alt = "install-asterisk"/>

После установки soft-телефона Zoiper5 на нем был совершен вход в аккаунт 1001:

Логин: 1001

Пароль: 111

Адрес сервера: 127.0.0.1 

Для того, чтобы проверить назначение порта аккаунту 1001 был перезапущен Asterisk. Из рисунка видно, что адрес 127.0.0.1 появился в перечне аккаунтов:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/4.png" width = "700" height = "300" alt = "install-asterisk"/>

Следующим шагом была произведена установка MicroSIP, после чего в нем был создан новый аккаунт со следующими данными:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/5.png" width = "200" height = "400" alt = "install-asterisk"/>

После добавления аккаунта был совершен звонок с номера 1002 на номер 1001:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/6.png" width = "200" height = "400" alt = "install-asterisk"/>

Звонок был успешно получен:

<img src = "https://github.com/IuliiaNikitina1/2023_2024-ip-telephony-k34212-nikitina_i_a/blob/main/lab3/images/7.png" width = "700" height = "300" alt = "install-asterisk"/>


#### 3. Вывод:

Таким образом, в ходе выполнения лабораторной работы был установлен и изучен программный комплекс Asterisk. С помощью soft-телефонов Zoiper5 и MicroSIP были созданы два SIP-аккаунта 1001 и 1002, между которыми путем локального звонка было успешно установлено соединение.  




