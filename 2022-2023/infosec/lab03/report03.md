---
# Front matter
lang: ru-RU
title: "Лабораторная работа №3"
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

Получение практических навыков работы в консоли с атрибутами файлов для
групп пользователей.

# Задание

Часть 1 (Консоль)
Создаем гостя2 и добавляем его в группу 


Часть 2 (Работа с правами доступа)
Заполняем таблицы


# Выполнение лабораторной работы

В установленной при выполнении предыдущей лабораторной работы создала учётную запись пользователя guest2 с помощью команды “sudo useradd guest2” и
задала пароль для этого пользователя командой “sudo passwd guest2”. Добавила
пользователя guest2 в группу guest с помощью команды “sudo gpasswd -a guest2
guest” (рис. [-@fig:001])


![Другая учетная запись](image/1.png){ #fig:001 width=70% }

Затем осуществила вход в систему от двух пользователей на двух разных консолях при помощи команд “su guest” и “su guest2”. Определила командой “pwd”,
что оба пользователя находятся в своих домашних директориях, что совпадает с
приглашениями командной строки. Уточнила имена пользователей командой
“whoami”, соответственно получила: guest и guest2. С помощью команд “groups
guest” и “groups guest2” определила, что пользователь guest входит в группу guest,
а пользователь guest2 в группы guest и guest2. Сравнила полученную информацию с выводом команд “id -Gn guest”, “id -Gn guest2”, “id -G guest” и “id -G guest2”:
данные совпали, за исключением второй команды “id -G”, которая вывела номера
групп 1001 и 1002, что также является верным (рис. [-@fig:002])

![Проверка учетных записей](image/2.png){ #fig:002 width=70% }



От имени пользователя guest2 зарегистрировала этого пользователя в группе
guest командой “newgrp guest”. Далее от имени пользователя guest изменила
права директории /home/guest, разрешив все действия для пользователей группы
командой “chmod g+rwx /home/guest”. Сняла с директории /home/guest/dir1 все атрибуты командой “chmod 000 dir1” и проверила
правильность снятия атрибутов командой “ls -l” (рис. [-@fig:003])


![Атрибуты](image/3.png){ #fig:003 width=70% }

Теперь заполним таблицу «Установленные права и разрешённые действия»
(рис. [-@fig:004]), меняя атрибуты у директории и файла от имени пользователя guest и делая
проверку от пользователя guest2.

Создание файла: “echo”text” > /home/guest/dir1/file2”
Удаление файла: “rm -r /home/guest/dir1/file1”
Запись в файл: “echo”textnew” > /home/guest/dir1/file1”
Чтение файла: “cat /home/guest/dir1/file1”
Смена директории: “cd /home/guest/dir1”
Просмотр файлов в директории: “ls /home/guest/dir1”
Переименование файла: “mv /home/guest/dir1/file1 filenew”
Смена атрибутов файла: “chattr -a /home/guest/dir1/file1”


Таблица 1 

![Таблица1](image/table1-1.png){ #fig:004 width=70% }
![Таблица1](image/table1-2.png){ #fig:005 width=70% }
![Таблица1](image/table1-3.png){ #fig:006 width=70% }
![Таблица1](image/table1-4.png){ #fig:007 width=70% }
![Таблица1](image/table1-5.png){ #fig:008 width=70% }
![Таблица1](image/table1-6.png){ #fig:009 width=70% }
![Таблица1](image/table1-7.png){ #fig:010 width=70% }
![Таблица1](image/table1-8.png){ #fig:011 width=70% }

Таблица 2
![Таблица2](image/table2.png){ #fig:012 width=70% }




# Выводы

В ходе выполнения данной лабораторной работы я получила практические
навыки работы в консоли с атрибутами файлов для групп пользователей.

# Список литературы

Лабораторная работа №3

Права доступа к файлам в Linux [Электронный ресурс]. 2019. URL: https:
//losst.ru/prava-dostupa-k-fajlam-v-linux.

