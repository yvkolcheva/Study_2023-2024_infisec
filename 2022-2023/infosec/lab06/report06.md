---
# Front matter
lang: ru-RU
title: "Лабораторная работа №6"
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

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux. Проверить работу SELinux на практике совместно с веб-сервером Apache.


# Выполнение лабораторной работы

Вошла в систему под своей учетной записью и убедилась, что SELinux работает
в режиме enforcing политики targeted с помощью команд “getenforce” и “sestatus”(рис. [-@fig:001])


![Ввод команд](image/1.png){ #fig:001 width=70% }


Обратилась с помощью браузера к веб-серверу, запущенному на моем компьютере, и убедилась, что последний работает с помощью команды “service httpd
status” (рис. [-@fig:002])

![Обращение к веб-серверу](image/2.png){ #fig:002 width=70% }

С помощью команды “ps auxZ | grep httpd” определила контекст безопасности
веб-сервера Apache - httpd_t (рис. [-@fig:003])

![Контекст безопасности](image/3.png){ #fig:003 width=70% }


Посмотрела текущее состояние переключателей SELinux для Apache с помощью команды “sestatus -bigrep httpd”. Посмотрела статистику по политике с помощью команды “seinfo”. Множество
пользователей - 8, ролей - 14, типов 4995 (рис. [-@fig:004])

![Состояние](image/4.png){ #fig:004 width=70% }

С помощью команды “ls -lZ /var/www” посмотрела файлы и поддиректории,
находящиеся в директории /var/www. Используя команду “ls -lZ /var/www/html”,
определила, что в данной директории файлов нет. Только владелец/суперпользователь может создавать файлы в директории /var/www/html (рис. [-@fig:005])

![Просмотр](image/5.png){ #fig:005 width=70% }

От имени суперпользователя создала html-файл /var/www/html/test.html. Контекст созданного файла - httpd_sys_content_t  (рис. [-@fig:007])

![Создание и написание](image/6.png){ #fig:006 width=70% }

Обратилась к файлу через веб-сервер, введя в браузере адрес “http://127.0.0.1/test.html”.
Файл был успешно отображен  (рис. [-@fig:008])

![Обращение](image/7.png){ #fig:007 width=70% }

Изучив справку man httpd_selinux, выяснила, что для httpd определены следующие контексты файлов: httpd_sys_content_t, httpd_sys_script_exec_t,
httpd_sys_script_ro_t, httpd_sys_script_rw_t, httpd_sys_script_ra_t, httpd_unconfined_script_exec_t.
Контекст моего файла - httpd_sys_content_t (в таком случае содержимое должно
быть доступно для всех скриптов httpd и для самого демона). Изменила
контекст файла на samba_share_t командой “sudo chcon -t samba_share_t
/var/www/html/test.html” и проверила, что контекст поменялся (рис. [-@fig:008])

![Просмотр](image/8.png){ #fig:008 width=70% }

Попробовала еще раз получить доступ к файлу через веб-сервер, введя в браузере адрес “http://127.0.0.1/test.html” и получила сообщение об ошибке (т.к. к
установленному ранее контексту процесс httpd не имеет доступа)  (рис. [-@fig:009])

![Ошибка](image/9.png){ #fig:009 width=70% }

Командой “ls -l /var/www/html/test.html” убедилась, что читать данный файл может любой пользователь. Просмотрела системный лог-файл веб-сервера Apache
командой “sudo tail /var/log/messages”, отображающий ошибки   (рис. [-@fig:010])

![Работа с консолью](image/10.png){ #fig:010 width=70% }

В файле /etc/httpd/conf/httpd.conf заменила строчку “Listen 80” на “Listen 81”,
чтобы установить веб-сервер Apache на прослушивание TCP-порта 81  (рис. [-@fig:011])

![Замена строки](image/11.png){ #fig:011 width=70% }

Перезапускаем веб-сервер Apache и анализируем лог-файлы командой “tail -nl
/var/log/messages” [-@fig:012])

![Перезапуск](image/12.png){ #fig:012 width=70% }

Просмотрела файлы “var/log/http/error_log”, “/var/log/http/access_log” и
“/var/log/audit/audit.log” и выяснила, что запись появилась в последнем файле  (рис. [-@fig:013])

![Содержание файла](image/13.png){ #fig:0013 width=70% }

Выполнила команду “semanage port -a -t http_port_t -р tcp 81” и убедилась, что
порт TCP-81 установлен. Проверила список портов командой “semanage port -l
| grep http_port_t”, убедилась, что порт 81 есть в списке и запускаем веб-сервер
Apache снова (рис. [-@fig:014]) 

![Работа с консолью](image/14.png){ #fig:014 width=70% }

Вернула контекст “httpd_sys_cоntent_t” файлу “/var/www/html/test.html” командой “chcon -t httpd_sys_content_t /var/www/html/test.html” (рис. 3.16) и после этого попробовала получить доступ к файлу через веб-сервер, введя адрес “http://127.0.0.1:81/test.html”, в результате чего увидела содежимое файла - слово
“test” (рис. [-@fig:015])(рис. [-@fig:016])

![Возвращение](image/15.png){ #fig:015 width=70% }

![Содержимое файла](image/16.png){ #fig:016 width=70% }

Исправила обратно конфигурационный файл apache, вернув “Listen 80”. Попыталась удалить привязку http_port к 81 порту командой “semanage port -d -t
http_port_t -p tcp 81”, но этот порт определен на уровне политики, поэтому его
нельзя удалить (рис. [-@fig:017])

![Попытка удаления](image/17.png){ #fig:017 width=70% }

Удалила файл “/var/www/html/test.html” командой “rm /var/www/html/test.html” (рис. [-@fig:017])

![Удаление файла](image/18.png){ #fig:018 width=70% }



# Выводы

В ходе выполнения данной лабораторной работы я развила навыки администрирования ОС Linux, получила первое практическое знакомство с технологией SELinux и проверила работу SELinux на практике совместно с веб-сервером Apache.

# Список литературы

Лабораторная работа №6

SELinux – описание и особенности работы с системой [Электронный ресурс]. URL: https://habr.com/ru/company/kingservers/blog/209644/.

