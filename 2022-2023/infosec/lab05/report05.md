---
# Front matter
lang: ru-RU
title: "Лабораторная работа №5"
subtitle: "Основы информационной безопасности"
author: "Колчева Юлия Вячеславовна"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучение механизмов изменения идентификаторов, применения SetUID- и
Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление
файлов.

# Задание

Часть 1 

Создание программы


Часть 2 

Исследование Sticky-бита


# Выполнение лабораторной работы

Для начала я убедилась, что компилятор gcc установлен, исолпьзуя команду
“gcc -v”. Затем отключила систему запретов до очередной перезагрузки системы
командой “sudo setenforce 0”, после чего команда “getenforce” вывела “Permissive”(рис. [-@fig:001])


![Работа с консолью](image/1.png){ #fig:001 width=70% }


Проверила успешное выполнение команд “whereis gcc” и “whereis g++” (их расположение) (рис. [-@fig:002])

![Работа с консолью](image/2.png){ #fig:002 width=70% }

Вошла в систему от имени пользователя guest командой “su - guest”. Создала программу simpleid.c командой “touch simpleid.c” и открыла её в редакторе
командой “gedit /home/guest/simpleid.c” (рис. [-@fig:003])

![Работа с консолью](image/3.png){ #fig:003 width=70% }


Код программы выглядит следующим образом (рис. [-@fig:004])


![Код первой программы](image/4.png){ #fig:004 width=70% }

Скомпилировала программу и убедилась, что файл программы был создан
командой “gcc simpleid.c -o simpleid”. Выполнила программу simpleid командой
“./simpleid”, а затем выполнила системную программу id командой “id”. Результаты, полученные в результате выполнения обеих команд, совпадают (uid=1001 и
gid=1001) (рис. [-@fig:005])

![Работа с консолью](image/5.png){ #fig:005 width=70% }

Усложнила программу, добавив вывод действительных идентификаторов  (рис. [-@fig:007])

![Вторая программа](image/6.png){ #fig:006 width=70% }

Получившуюся программу назвала simpleid2.c  (рис. [-@fig:008])

![Работа с консолью](image/7.png){ #fig:007 width=70% }

Скомпилировала и запустила simpleid2.c командами “gcc simpleid2.c -o sipleid2”
и “./simpleid2”  (рис. [-@fig:008])

![Работа с консолью](image/8.png){ #fig:008 width=70% }

От имени суперпользователя выполнила команды “sudo chown root:guest
/home/guest/simpleid2” и “sudo chmod u+s /home/guest/simpleid2”, затем выполнила проверку правильности установки новых атрибутов и смены владельца
файла simpleid2 командой “sudo ls -l /home/guest/simpleid2” (рис. 3.9). Этими
командами была произведена смена пользователя файла на root и установлен
SetUID-бит.  (рис. [-@fig:009])

![Работа с консолью](image/9.png){ #fig:009 width=70% }

Запустила программы simpleid2 и id. Теперь появились различия в uid  (рис. [-@fig:010])

![Работа с консолью](image/10.png){ #fig:010 width=70% }

Проделала тоже самое относительно SetGID-бита. Также можем заметить различия с предыдущим пунктом  (рис. [-@fig:011]) (рис. [-@fig:012])

![Работа с консолью](image/11.png){ #fig:011 width=70% }

![Работа с консолью](image/12.png){ #fig:012 width=70% }

Создаем программу readfile.c  (рис. [-@fig:013])

![Работа с консолью](image/13.png){ #fig:0013 width=70% }

Скомпилировала созданную программу командой “gcc readfile.c -o readfile”.
Сменила владельца у файла readfile.c командой “sudo chown root:guest
/home/guest/readfile.c” и поменяла права так, чтобы только суперпользователь
мог прочитать его, а guest не мог, с помощью команды “sudo chmod 700
/home/guest/readfile.c”. Теперь убедилась, что пользователь guest не может
прочитать файл readfile.c командой “cat readfile.c”, получив отказ в доступе (рис. [-@fig:014]) (рис. [-@fig:015])

![Работа с консолью](image/14.png){ #fig:014 width=70% }

![Работа с консолью](image/15.png){ #fig:015 width=70% }


Поменяла владельца у программы readfile и устанавила SetUID. Проверила, может ли программа readfile прочитать файл readfile.c командой “./readfile readfile.c”.
Прочитать удалось.Аналогично проверила, можно ли прочитать файл /etc/shadow.
Прочитать удалось (рис. [-@fig:016])

![Работа с консолью](image/16.png){ #fig:016 width=70% }

2 часть 

Командой “ls -l / | grep tmp” убеждилась, что атрибут Sticky на директории /tmp
установлен. От имени пользователя guest создала файл file01.txt в директории
/tmp со словом test командой “echo”test” > /tmp/file01.txt”. Просматрела атрибуты
у только что созданного файла и разрешаем чтение и запись для категории
пользователей “все остальные” командами “ls -l /tmp/file01.txt” и “chmod o+rw
/tmp/file01.txt” (рис. [-@fig:017])

![Работа с консолью](image/17.png){ #fig:017 width=70% }

От имени пользователя guest2 попробовала прочитать файл командой “cat
/tmp/file01.txt” - это удалось. Далее попыталась дозаписать в файл слово test2,
проверить содержимое файла и записать в файл слово test3, стерев при этом всю
имеющуюся в файле информацию - эти операции удалось выполнить только в
случае, если еще дополнительно разрешить чтение и запись для группы пользователей командой “chmod g+rw /tmp/file01.txt”. От имени пользователя guest2
попробовала удалить файл - это не удается ни в каком из случаев, возникает
ошибка (рис. [-@fig:018])

![Работа с консолью](image/18.png){ #fig:018 width=70% }

Повысила права до суперпользователя командой “su -” и выполнила команду,
снимающую атрибут t с директории /tmp “chmod -t /tmp”. После чего покинула
режим суперпользователя командой “exit”. Повторила предыдущие шаги. Теперь
мне удалось удалить файл file01.txt от имени пользователя, не являющегося его
владельцем (рис. [-@fig:019])

![Работа с консолью](image/19.png){ #fig:019 width=70% }

Повысила свои права до суперпользователя и вернула атрибут t на директорию
/tmp (рис. [-@fig:020])

![Работа с консолью](image/20.png){ #fig:020 width=70% }


# Выводы

В ходе выполнения данной лабораторной работы я изучила механизмы изменения идентификаторов, применение SetUID- и Sticky-битов. Получила практические навыки работы в консоли с дополнительными атрибутами. Рассмотрела
работу механизма смены идентификатора процессов пользователей, а также
влияние бита Sticky на запись и удаление файлов.


# Список литературы

Лабораторная работа №5

Стандартные права SetUID, SetGID, Sticky в Linux [Электронный ресурс].
URL: https://linux-notes.org/standartny-e-prava-unix-suid-sgid-sticky-bity/
