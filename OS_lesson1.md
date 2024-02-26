# Домашнее задание к занятию «Операционные системы. Лекция 1»

1. Какой системный вызов делает команда `cd`? 

    В прошлом ДЗ вы выяснили, что `cd` не является самостоятельной  программой. Это `shell builtin`, поэтому запустить `strace` непосредственно на `cd` не получится. Вы можете запустить `strace` на `/bin/bash -c 'cd /tmp'`. В этом случае увидите полный список системных вызовов, которые делает сам `bash` при старте. 

    Вам нужно найти тот единственный, который относится именно к `cd`. Обратите внимание, что `strace` выдаёт результат своей работы в поток stderr, а не в stdout.

### Ответ

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_10.png "strace cd")

2. Попробуйте использовать команду `file` на объекты разных типов в файловой системе. Например:

    ```bash
    vagrant@netology1:~$ file /dev/tty
    /dev/tty: character special (5/0)
    vagrant@netology1:~$ file /dev/sda
    /dev/sda: block special (8/0)
    vagrant@netology1:~$ file /bin/bash
    /bin/bash: ELF 64-bit LSB shared object, x86-64
    ```
    
    Используя `strace`, выясните, где находится база данных `file`, на основании которой она делает свои догадки.

### Ответ

**Если смотреть на openat строки, то там постоянно появляется какой-то magic. И, как я поняла по man magic,  к его библиотекам и базе обращается не только file, но и type, и test. А может и нет - почитаю еще**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_11.png "strace file")

3. Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удалён (deleted в lsof), но сказать сигналом приложению переоткрыть файлы или просто перезапустить приложение возможности нет. Так как приложение продолжает писать в удалённый файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков, предложите способ обнуления открытого удалённого файла, чтобы освободить место на файловой системе.

### Ответ

**Понимаю суть задания, но не понимаю как воспроизвести полноценно для скринов, чтоб писало что-то в файл. Сделала файлик с небольшим количеством строк просто чтоб был какой-то объем, открыла его в vi и отправила в фон ctrl-z. Удалила сам файл, остался висеть процесс и его swp. Отправила на pid процесса эхо с пустотой и он висит теперь явно без содержимого:**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_14.png "to_delete")

4. Занимают ли зомби-процессы ресурсы в ОС (CPU, RAM, IO)?

### Ответ

**Нет, кроме того, что висит строка в таблице процессов - сам процесс уже завершен с непонятным кодом возврата, если он в статусе зомби**

5. В IO Visor BCC есть утилита `opensnoop`:

    ```bash
    root@vagrant:~# dpkg -L bpfcc-tools | grep sbin/opensnoop
    /usr/sbin/opensnoop-bpfcc
    ```
    
    На какие файлы вы увидели вызовы группы `open` за первую секунду работы утилиты? Воспользуйтесь пакетом `bpfcc-tools` для Ubuntu 20.04. Дополнительные сведения по установке [по ссылке](https://github.com/iovisor/bcc/blob/master/INSTALL.md).

### Ответ

**В первую секунду работы утилиты он вывел несколько одинаковых сообщений такого типа:**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_15.png "snoop")

**А потом началась большая портянка из процессов:**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_16.png "snoop")

**С аргументом -d 1 он остановился вот тут:**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_17.png "snoop")

6. Какой системный вызов использует `uname -a`? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в `/proc` и где можно узнать версию ядра и релиз ОС.

### Ответ

**-a  - это all, то есть все, кроме -p и -i:**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_18.png "snoop")

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_22.png "snoop")

**Совпадает! Только -m аргумент будто три раза в -а выводится** 

**Он меня за полным маном почему-то отправил в интернеты. По ссылке вот такая информация:**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_21.png "snoop")

**Пришлось поискать. И далеко не все из описанного табается**

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_233.png "snoop")

7. Чем отличается последовательность команд через `;` и через `&&` в bash? Например:

    ```bash
    root@netology1:~# test -d /tmp/some_dir; echo Hi
    Hi
    root@netology1:~# test -d /tmp/some_dir && echo Hi
    root@netology1:~#
    ```
    
    Есть ли смысл использовать в bash `&&`, если применить `set -e`?

### Ответ

**Через ; команды выполняются просто последовательно без каких-либо требований к кодам возврата друг друга. А через && не вывел эхо, потому что в левой части код возврата не 0, то есть такой директории не было. Выражение И (&&) выполнится только если все соединенные им выражения отдают 0, если бы было ИЛИ (||), до тостаточно чтобы выполнился хоть один. **

> -e  Exit immediately if a command exits with a non-zero status.

**То есть с set -e будет прерываться выполнение череды команд, если одна из них вернет не 0. А соединенные И они продолжат выполнятся, но в итоге все равно не выведут результат. Значит, имеет смысл для экономии вычислительных ресурсов использовать ; с set-e вместо &&**

8. Из каких опций состоит режим bash `set -euxo pipefail`, и почему его хорошо было бы использовать в сценариях?

### Ответ

>-e  Exit immediately if a command exits with a non-zero status.  
>-u  Treat unset variables as an error when substituting.  
>-x  Print commands and their arguments as they are executed.  
>-o option-name  
>     pipefail       
>     the return value of a pipeline is the status of  
>     the last command to exit with a non-zero status,    
>     or zero if no command exited with a non-zero status  

**То  есть, он прерывает, если появлется код возврата отличный от 0; проверяет заданные переменные; пихает все команды в стандартный вывод (поможет увидеть где споткнулись) и возвращает статус всего пайплайна, а не только последнего выполненного. Выглядит очень удобно для скриптов**

9. Используя `-o stat` для `ps`, определите, какой наиболее часто встречающийся статус у процессов в системе. В `man ps` изучите (`/PROCESS STATE CODES`), что значат дополнительные к основной заглавной букве статуса процессов. Его можно не учитывать при расчёте (считать S, Ss или Ssl равнозначными).

### Ответ

![скрин](https://github.com/Jlljully/devops_netology3/blob/main/Screenshot_24.png "stat")

>R    running or runnable (on run queue)  
>S    interruptible sleep (waiting for an event to complete)  
>\+    is in the foreground process group  
>s    is a session leader

**То есть STAT - просто заголовок, R - процессы запущенные или в очереди выполнения, S - в состоянии сна. + - это дополнителный символ что процесс на переднем плане, s - что это лидер сеанса(?)**
