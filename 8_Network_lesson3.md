# Домашнее задание к занятию «Компьютерные сети. Лекция 3»

1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP.

 ```
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```

### Ответ

**Почему-то команда с указанием маски не выполняется. И если указать не свой айпи, а шлюз (что показалось логичным: маску для сети всей указываем же) - тоже не работает. Вот так сработал:**

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_3.png "1")

2. Создайте dummy-интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.

### Ответ

**Неактуальные методички, не адаптированные под ubuntu, с которой начинали работать в прошлых модулях. Я бы предложила ссылку добавить в презу [такую](https://super-unix.com/ubuntu/ubuntu-ubuntu-18-04-how-to-create-a-persistent-dumthe-network-interface/)**

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_4.png "Dummy")

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_5.png "Dummy")

**Маршруты пришлось добавлять с nmcli**

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_6.png "Route")

3. Проверьте открытые TCP-порты в Ubuntu. Какие протоколы и приложения используют эти порты? Приведите несколько примеров.

### Ответ

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_7.png "tcp")

**Еще, например, 20,21 - FTP, telnet - 23**

4. Проверьте используемые UDP-сокеты в Ubuntu. Какие протоколы и приложения используют эти порты?

### Ответ

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_9.png "udp")

5. Используя diagrams.net, создайте L3-диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 

### Ответ

![Скрин](https://github.com/Jlljully/Net_3/blob/main/Screenshot_10.png "домик")
