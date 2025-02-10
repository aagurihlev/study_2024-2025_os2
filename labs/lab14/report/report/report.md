---
## Front matter
title: "Лабораторная работа №14"
subtitle: "Партиции, файловые системы, монтирование"
author: "Гурылев Артем Андреевич"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Целью работы является получение навыков создания разделов на диске и файловых систем, а также монтирования этих файловых систем.

# Выполнение лабораторной работы

Добавим к нашей виртуальной машине диски, с которыми будем работать(рис. [-@fig:001]):

![Диски](image/1.png){#fig:001 width=70%}

Используем утилиту fdisk, чтобы посмотреть перечень разделов на всех системных дисках(рис. [-@fig:002]):

![Перечень разделов](image/2.png){#fig:002 width=70%}

Начнем использовать утилиту fdisk для работы с разделами. Выберем первый диск(/dev/sdb). Создадим основной раздел на 100 MiB и определим его тип как файловую систему Linux(рис. [-@fig:003]):

![Работа с fdisk](image/3.png){#fig:003 width=70%}

#Выполнение самостоятельной работы



# Выводы



# Контрольные вопросы



