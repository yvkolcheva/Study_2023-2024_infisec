---
# Front matter
lang: ru-RU
title: "Лабораторная работа №4"
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

Получение практических навыков работы в консоли с расширенными атрибутами файлов.

# Задание

Часть 1 
Работа с атрибутом a 


Часть 2 
Работа с атрибутом i


# Выполнение лабораторной работы

Вошла в учетную запись guest и определила расширенные атрибуты файла /home/guest/dir1/file1 командой “lsattr /home/guest/dir1/file1”. Командой
“chmod 600 /home/guest/dir1/file1” установила права, разрешающие чтение и
запись для владельца файла. При попытке использовать команду “chattr +a
/home/guest/dir1/file1” для установления расширенного атрибута “a” получила
отказ в выполнении операции (рис. [-@fig:001])(рис. [-@fig:002])


![Работа с консолью](image/1.png){ #fig:001 width=70% }

![Отказ](image/2.png){ #fig:002 width=70% }

Установила расширенный атрибут “a” на файл командой (от лица суперпользователя) “chattr +a /home/guest/dir1/file1” и от имени пользователя guest проверила правильность установления атрибута командой “lsattr /home/guest/dir1/file1” (рис. [-@fig:003]) (рис. [-@fig:004])

![Установка атрибута](image/3.png){ #fig:003 width=70% }

![Проверка](image/4.png){ #fig:004 width=70% }


Дозаписала в файл file1 слово “test” командой “echo”test” » /home/guest/dir1/file1”
и, используя команду “cat /home/guest/dir1/file1” убедилась, что указанное
ранее слово было успешно записано в наш файл. Аналогично записала в файл
слово “abcd”. Далее попробовала стереть имеющуюся в файле информацию
командой “echo”abcd” > /home/guest/dirl/file1”, но получила отказ. Попробовала
переименовать файл командой “rename file1 file2 /home/guest/dirl/file1” и
изменить права доступа командой “chmod 000 /home/guest/dirl/file1” и также
получила отказ (рис. [-@fig:005])


![Работа с файлом](image/5.png){ #fig:005 width=70% }

Сняла расширенный атрибут “a” с файла от имени суперпользователя командой
“sudo chattr -a /home/guest/dir1/file1” и повторила операции, они были выполнены. (рис. [-@fig:006])

![Работа с файлом](image/6.png){ #fig:006 width=70% }

От имени суперпользователя командой “chattr +i /home/guest/dir1/file1”
установила расширенный атрибут “i” и повторила действия, которые выполняла
ранее. В данном случае файл можно было только прочитать, остальные операции недоступны. (рис. [-@fig:007])

![Работа с файлом](image/7.png){ #fig:007 width=70% }

# Выводы

В ходе выполнения данной лабораторной работы я получила практические
навыки работы в консоли с расширенными атрибутами файлов, на практике
опробовала действие расширенных атрибутов “a” и “i”.

# Список литературы

Лабораторная работа №4

Права доступа к файлам в Linux [Электронный ресурс]. 2019. URL: https:
//losst.ru/prava-dostupa-k-fajlam-v-linux.

