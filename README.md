# Домашнее задание к занятию «Защита сети»
#### Грибанов Антон. FOPS-31

### Подготовка к выполнению заданий

1. Подготовка защищаемой системы:

- установите **Suricata**,
- установите **Fail2Ban**.

2. Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

#### Решение:
##### Установка Suricata
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_001.png)
##### Установка Fail2Ban
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_003.png)
##### Установка nmap и hydra
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_002.png)

------

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

#### Решение:

##### **sudo nmap -sA 192.168.2.171. 
*** Сканирование nmap -sA (ACK) в логи suricata не попало.

##### **sudo nmap -sT 192.168.2.171
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_004.png)

##### **sudo nmap -sS 192.168.2.171
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_005.png)

##### **sudo nmap -sV 192.168.2.171
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_006.png)

##### В логах fail2ban зафиксировано только сканирование nmap -sV
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_007.png)


------

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.

#### Решение:
##### Подбор пароля по ssh (fail2ban - до включения защиты ssh)
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_008.png)
![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_009.png)

##### Подбор пароля по ssh (fail2ban - после включения защиты ssh)

**статус fail2ban

![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_010.png)

**логи suricata

![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_011.png)

**логи auth.log

![13-03](https://github.com/Qshar1408/13-03/blob/main/img/hw_13_03_012.png)

*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*
