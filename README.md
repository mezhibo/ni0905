**Сетевая топология**

![Image alt](https://github.com/mezhibo/ni0905/blob/1db1d40f58b26a01ef69cec2ed1e487eeaca5638/IMG/1.png)


**Задание 1. Выполняется на R1**

1. Создать локального пользователя admin1 и пароль к нему admin1

2. Войти по telnet с терминала

3. Войти в привелигированный режим enable

4. Сохранить конфигурацию

5. Убедиться, что пароль сохранен в зашифрованном виде

6. Ответьте на вопрос: были ли проблемы при входе в привелигированный режим enable или другие проблемы, если были, то как решили? Если проблем не было, то какие могли бы быть?




**Решение 1**

```
username admin privilege 15 secret 5 $1$mERr$7n6je7c9FKvO.o.40Rj1Q0
username admin1 privilege 15 secret 5 $1$mERr$7n6je7c9FKvO.o.40Rj1Q0
username cisco1 privilege 15 secret 5 $1$mERr$q.MA2tj.WFptzvbifq/1i.
```

Вывод sh run

```
R1#show run
Building configuration...

Current configuration : 1667 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
enable secret 5 $1$mERr$7n6je7c9FKvO.o.40Rj1Q0
!
aaa new-model
!
aaa authentication login default local 
!
no ip cef
no ipv6 cef
!
username admin privilege 15 secret 5 $1$mERr$7n6je7c9FKvO.o.40Rj1Q0
username admin1 privilege 15 secret 5 $1$mERr$7n6je7c9FKvO.o.40Rj1Q0
username cisco1 privilege 15 secret 5 $1$mERr$q.MA2tj.WFptzvbifq/1i.
!
license udi pid CISCO2901/K9 sn FTX15242VED-
!
ip ssh version 2
no ip domain-lookup
ip domain-name netology.ru
!
spanning-tree mode pvst
!
interface GigabitEthernet0/0
 ip address 10.255.255.1 255.255.255.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 ip address 10.0.0.1 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/2/0
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/1
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/2
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/3
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/0
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/1
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/2
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/3
 switchport mode access
 switchport nonegotiate
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
line con 0
!
line aux 0
!
line vty 0 4
 login authentication default
!
end

```

Ответьте на вопрос: были ли проблемы при входе в привелигированный режим enable или другие проблемы, если были, то как решили? Если проблем не было, то какие могли бы быть?


Были проблемы, решились при помощи enable secret

**Задание 2. Выполняется на R2 и RADIUS_1**

1. Создать следующие настройки AAA на R2:

 - aaa new-model

 - aaa authentication login default group radius

 - radius-server host 10.0.0.4 auth-port 1645 key 123qwe

2. Создать на RADIUS_1 клиента R2 10.0.0.2 с ключом 123qwe

3. Создать на RADIUS_1 пользователя user1 с паролем user1

4. Войти на R2 в режим enable

5. Выключить сервер RADUIS_1

6. Войти на R2 по telnet

7.Ответить на вопрос: были ли проблемы при выполнении пунктов 4 и 6? Если были, то как решили? Если проблем не было, то какие могли бы быть?


**Решение 2**

Команда:

```
radius-server host 10.0.0.4 auth-port 1645 key 123qwe

```
не поддерживается оборудованием в лабе, настройки radius производятся другим способом.

Проблем не было, для избежания потери доступности оборудования был заведен локальный пользователь и включена возможность аутенфикации через локального пользователя в случая потери связи с radius


```
Router#show run
Building configuration...

Current configuration : 1575 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Router
!
enable secret 5 $1$mERr$vTbHul1N28cEp8lkLqr0f/
!
aaa new-model
!
aaa authentication login default group radius local 
!
no ip cef
no ipv6 cef
!
username admin privilege 15 secret 5 $1$mERr$vTbHul1N28cEp8lkLqr0f/
!
license udi pid CISCO2901/K9 sn FTX1524Q2T5-
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface GigabitEthernet0/0
 ip address 10.255.255.2 255.255.255.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 ip address 10.0.0.2 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/2/0
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/1
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/2
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/3
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/0
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/1
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/2
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/3
 switchport mode access
 switchport nonegotiate
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
radius server 10.0.0.4
 address ipv4 10.0.0.4 auth-port 1645
 key 123qwe
!
line con 0
!
line aux 0
!
line vty 0 4
 login authentication default
!
end
```


**Задание 3. Выполняется на R3 и RADIUS_1 и RADIUS_2.**

1. Выполнить на R3 все настройки из задания 1 и 2 (локальный пользователь и клиент серверов R3)

2. Создать конфигурацию AAA с резервированием серверов RADIUS

3. Проверить доступность R3 по telnet с поочередным отключением серверов 1 и 2

**Решение 3**

```
Router#show run
Building configuration...

Current configuration : 1794 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Router
!
enable secret 5 $1$mERr$vTbHul1N28cEp8lkLqr0f/
!
aaa new-model
!
aaa authentication login default group radius local 
!
no ip cef
no ipv6 cef
!
username admin privilege 15 secret 5 $1$mERr$vTbHul1N28cEp8lkLqr0f/
!
license udi pid CISCO2901/K9 sn FTX1524P2X8-
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface GigabitEthernet0/0
 ip address 10.255.255.3 255.255.255.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 ip address 10.0.0.3 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/2/0
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/1
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/2
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/2/3
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/0
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/1
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/2
 switchport mode access
 switchport nonegotiate
!
interface FastEthernet0/3/3
 switchport mode access
 switchport nonegotiate
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
radius server RADIUS_1
 address ipv4 10.0.0.4 auth-port 1645
 key 123qwe
radius server 10.0.0.4
 address ipv4 10.0.0.4 auth-port 1645
 key 123qwe
radius server RADIUS_2
 address ipv4 10.0.0.5 auth-port 1645
 key 123qwe
radius server 10.0.0.5
 address ipv4 10.0.0.5 auth-port 1645
 key 123qwe
!
line con 0
!
line aux 0
!
line vty 0 4
 login authentication default
!
end


Router# 
```

![Image alt](https://github.com/mezhibo/ni0905/blob/1db1d40f58b26a01ef69cec2ed1e487eeaca5638/IMG/2.png)
