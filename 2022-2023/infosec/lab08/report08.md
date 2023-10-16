---
# Front matter
lang: ru-RU
title: "Лабораторная работа №8"
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

Освоить на практике применение режима однократного гаммирования на примере кодирования различных исходных текстов одним ключом.

# Теоритическое введение

Гаммирование - наложение (снятие) на открытые (зашифрованные) данные
последовательности элементов других данных, полученной с помощью некоторого криптографического алгоритма, для получения зашифрованных (открытых) данных.

Основная формула, необходимая для реализации однократного гаммирования:
Ci = Pi XOR Ki, где Ci - i-й символ зашифрованного текста, Pi - i-й символ открытого текста, Ki - i-й символ ключа.

В данном случае для двух шифротекстов будет две формулы:

 С1 = P1 xor K и С2 =P2 xor K,

где индексы обозначают первый и второй шифротексты соответственно.

Если нам известны оба шифротекста и один открытый текст, то мы можем найти другой открытый текст, это следует из следующих формул:

 C1 xor C2 = P1 xor K xor P2 xor K = P1 xor P2,

 C1 xor C2 xor P1 = P1 xor P2 xor P1 = P2.


# Выполнение лабораторной работы

Код программы для выполнения задания.(рис. [-@fig:001])


![Код программы](image/1.png){ #fig:001 width=70% }

1-2 строки: импорт необходимых библиотек

4-10 строки: функция, реализующая сложение по модулю два двух строк

12-13: открытые/исходные тексты

15-16: создание ключа той же длины, что и открытый текст

22-23: получение шифротекстов с помощью функции, созданной ранее, при условии, что известны открытые тексты и ключ

26-27: получение открытых текстов с помощью функции, созданной ранее, при условии, что известны шифротексты и ключ

Результат работы программы можно увидеть на следующем скриншоте (рис. [-@fig:002])

![Результат работы](image/2.png){ #fig:001 width=70% }

Теперь попробуем реализовать "взлом" текстов при помощи операции XOR и без использования ключа. (рис. [-@fig:003])

!["Взлом" текстов](image/3.png){ #fig:002 width=70% }

31: сложение по модулю два двух шифротекстов с помощию функции,
созданной ранее.

33-34: получение открытых текстов с помощью функции, созданной ранее,
при условии, что известны оба шифротекста и один из открытых текстов.

Как видно на скриншоте, при помощи текста 1 мы можем получить текст 2 и наоборот. (рис. [-@fig:004])

!["Взлом" текстов](image/4.png){ #fig:004 width=70% }




# Выводы

В ходе выполнения данной лабораторной работы я освоила на практике применение режима однократного гаммирования на примере кодирования различных исходных текстов одним ключом.



# Список литературы

Лабораторная работа №8

Однократное гаммирование [Электронный ресурс]. URL: https://esystem.
rudn.ru/pluginfile.php/1651641/mod_resource/content/2/008-lab_cryptokey.pdf.

