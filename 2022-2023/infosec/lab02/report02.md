---
# Front matter
lang: ru-RU
title: "Лабораторная работа №2"
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

Получение практических навыков работы в консоли с атрибутами файлов, закрепление теоретических основ дискреционного разграничения доступа в современных системах с открытым кодом на базе ОС Linuxn.

# Задание

Часть 1 (Консоль)
Учимся работать с командной строкой 


Часть 2 (Работа с правами доступа)
Заполняем таблицы


# Выполнение лабораторной работы

В установленной при выполнении предыдущей лабораторной работы ОС создала учётную запись пользователя guest с помощью команды “sudo useradd guest”
и задала пароль для этого пользователя командой “sudo passwd guest” 


![Другая учетная запись](image/1.png){ #fig:001 width=70% }

Вошла в систему от имени пользователя guest (рис. 3.2, 3.3)

![Учетная запись](image/2.png){ #fig:002 width=70% }

Командой “pwd” определила, что нахожусь в директории /home/guest, которая
и является моей домашней директорией (рис. 3.4). С приглашением командной строки совпадает.
Уточнила имя моего пользователя командой “whoami” и получила вывод: guest
(рис. 3.4).
С помощью команды “id” определила имя своего пользователя - всё так же guest,
uid = 1001 (guest), gid = 1001 (guest). Затем сравнила полученную информацию с
выводом команды “groups”, которая вывела “guest”. Мой пользователь входит
только в одну группу, состоящую из него самого, поэтому вывод обеих команд “id”
и “groups” совпадает (рис. 3.4). Данные, выводимые в приглашении командной
строки, совпадают с полученной информацией.
Затем просмотрела файл /etc/passwd командой “cat /etc/passwd” (рис. 3.4).


![Команды](image/3.png){ #fig:003 width=70% }



Посмотрела, какие директории существуют в системе командой “ls -l /home/”
(рис. 3.6). Список поддиректорий директории /home получить удалось. На директориях установлены права чтения, записи и выполнения для самого пользователя
(для группы и остальных пользователей никаких прав доступа не установлено).
Проверила, какие расширенные атрибуты установлены на поддиректориях,
находящихся в директории /home, командой “lsattr /home” (рис. 3.6). Удалось
увидеть расширенные атрибуты только директории того пользователя, от имени
которого я нахожусь в системе.
Создала в домашней директории поддиректорию dir1 командой “mkdir dir1”
и определила, какие права доступа и расширенные атрибуты были на неё выставлены: чтение, запись и выполнение доступны для самого пользователя и для
группы, для остальных - только чтение и выполнение, расширенных атрибутов
не установлено (рис. 3.6).


![Работа с командной строкой](image/4.png){ #fig:004 width=70% }

Сняла с директории dir1 все атрибуты командой “chmod 000 dir1” и проверила
с её помощью правильность выполнения команды “ls -l”. Действительно, все
атрибуты были сняты (рис. 3.7).
Попыталась создать в директории dir1 файл file1 командой echo “test” >
/home/guest/dir1/file1 (рис. 3.7). Этого сделать не получилось, т.к. предыдущим
действием мы убрали право доступа на запись в директории. В итоге файл не
был создан (открыть директорию с помощью команды “ls -l /home/guest/dir1”
изначально тоже не удалось по той же причине, поэтому я поменяла права
доступа и снова воспользовалась этой командой, и тогда смогла просмотреть
содержимое директории, убедившись, что файл не был создан).


![Работа папкой](image/5.png){ #fig:005 width=70% }
![Отказ](image/6.png){ #fig:006 width=70% }

Задание

Заполним таблицу «Установленные права и разрешённые действия» 3.1.
Создание файла: “echo”text” > /home/guest/dir1/file2”
Удаление файла: “rm -r /home/guest/dir1/file1”
Запись в файл: “echo”textnew” > /home/guest/dir1/file1”
Чтение файла: “cat /home/guest/dir1/file1”
Смена директории: “cd dir1”
Просмотр файлов в директории: “ls dir1”
Переименование файла: “mv /home/guest/dir1/file1 filenew”
Смена атрибутов файла: “chattr -a /home/guest/dir1/file1”


![Таблица1](image/table1-1.png){ #fig:007 width=70% }
![Таблица1](image/table1-2.png){ #fig:008 width=70% }
![Таблица1](image/table1-3.png){ #fig:009 width=70% }
![Таблица1](image/table1-4.png){ #fig:010 width=70% }
![Таблица1](image/table1-5.png){ #fig:011 width=70% }
![Таблица1](image/table1-6.png){ #fig:012 width=70% }
![Таблица1](image/table1-7.png){ #fig:013 width=70% }
![Таблица1](image/table1-8.png){ #fig:014 width=70% }

Таблица 2
![Таблица2](image/table2.png){ #fig:015 width=70% }




# Выводы

В ходе выполнения данной лабораторной работы я приобрела практические
навыки работы в консоли с атрибутами файлов, закрепила теоретические основы
дискреционного разграничения доступа в современных системах с открытым
кодом на базе ОС Linux.

# Список литературы

Лабораторная работа №2 

