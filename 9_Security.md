# Домашнее задание к занятию «Элементы безопасности информационных систем»

## Задание

1. Установите плагин Bitwarden для браузера. Зарегестрируйтесь и сохраните несколько паролей.

### Ответ

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_6.png "Поставлен")

2. Установите Google Authenticator на мобильный телефон. Настройте вход в Bitwarden-акаунт через Google Authenticator OTP.

### Ответ

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_7.png "Привязан")

3. Установите apache2, сгенерируйте самоподписанный сертификат, настройте тестовый сайт для работы по HTTPS.

### Ответ

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_10.png "Апач стартован")

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_9.png "Ключ сгенерен")

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_8.png "Всем сайтам сайт!")

4. Проверьте на TLS-уязвимости произвольный сайт в интернете (кроме сайтов МВД, ФСБ, МинОбр, НацБанк, РосКосмос, РосАтом, РосНАНО и любых госкомпаний, объектов КИИ, ВПК и т. п.).

### Ответ

**Потестировала себя:**

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_11.png "Тест")

5. Установите на Ubuntu SSH-сервер, сгенерируйте новый приватный ключ. Скопируйте свой публичный ключ на другой сервер. Подключитесь к серверу по SSH-ключу.
 
### Ответ

**С одной своей ВМ на другую:**

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_13.png "Тест")

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_12.png "Тест")

6. Переименуйте файлы ключей из задания 5. Настройте файл конфигурации SSH-клиента так, чтобы вход на удалённый сервер осуществлялся по имени сервера.

### Ответ

**Переименовала mv оба файла в bubu и добавила конфиг файл:**

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_141.png "Переименование")

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_15.png "выход-вход")

**Судя по всему, ожидалось, что мы получим ошибку как на 23 слайде презы, но у меня с новой загрузкой вторая машина с другим айпи, может поэтому, никакой ошибки не получилось создать, он просто еще раз добавил ее в known host**

7. Соберите дамп трафика утилитой tcpdump в формате pcap, 100 пакетов. Откройте файл pcap в Wireshark.

### Ответ

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_16.png "Дамп")

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_17.png "Дамп")

 ---
 
## Задание со звёздочкой* 

Это самостоятельное задание, его выполнение необязательно.

8. Просканируйте хост scanme.nmap.org. Какие сервисы запущены?

### Ответ

**Открыты 22 - ssh, 80 - http, 9929 - nping-echo, 31337 - tcpwrapped** 

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_18.png "Скан")

9. Установите и настройте фаервол UFW на веб-сервер из задания 3. Откройте доступ снаружи только к портам 22, 80, 443.

### Ответ

![Скрин](https://github.com/Jlljully/Security/blob/main/Screenshot_19.png "Фаервол")
