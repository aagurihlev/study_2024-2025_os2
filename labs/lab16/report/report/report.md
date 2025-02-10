---
## Front matter
title: "Лабораторная работа №16"
subtitle: "Управление логическими томами"
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
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
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

Целью работы является освоение работы с RAID-массивами при помощи утилиты mdadm.

# Выполнение лабораторной работы

После получения полномочий администратора проверим наличие созданных дисков, а затем создадим на каждом из них раздел типа Linux, как указывает команда sfdisk.(рис. [-@fig:001]):

![Создание разделов](image/1.png){#fig:001 width=70%}

Дополнительно проверим тип раздела командой sfdisk. 83 - код раздела файловой системы Linux(рис. [-@fig:002]):

![Тип разделов](image/2.png){#fig:002 width=70%}

Посмотрим, какие типы партиций RAID можно задать, после чего установим этот тип разделов в каждой новой партиции.(рис. [-@fig:003]):

![Установка типов разделов на RAID](image/3.png){#fig:003 width=70%}

Посмотрим состояние дисков. Каждый из них имеет тип раздела Linux raid autodetect, сам раздел занимает почти весь размер в 512 MiB, а также у диска есть метка dos(рис. [-@fig:004]):

![Состояние дисков](image/4.png){#fig:004 width=70%}

Создадим массив RAID 1 из двух дисков с помощью утилиты mdadm(рис. [-@fig:005]):

![Создание массива](image/5.png){#fig:005 width=70%}

Проверии состояние массива с помощью команд cat и mdadm. В состоянии видно, что массив первого типа, он состоит из двух дисков без запасок, и что он размером в 510 MiB(рис. [-@fig:006]):

![Состояние массива](image/6.png){#fig:006 width=70%}

Создадим файловую систему ext4 для массива(рис. [-@fig:007]):

![Создание файловой системы](image/7.png){#fig:007 width=70%}

Подмонтируем массив(рис. [-@fig:008]):

![Монтирование массива](image/8.png){#fig:008 width=70%}

Добавим запись в fstab для автомонтирования(рис. [-@fig:009]):

![Файл fstab](image/9.png){#fig:009 width=70%}

Сымитируем сбой одного из дисков, после чего удалим этот сбойный диск и заменим его другим(рис. [-@fig:010]):

![Работа с дисками в массиве](image/10.png){#fig:010 width=70%}

Посмотрим состояние массива. Как можно увидеть, массив все также имеет два рабочих устройства, поскольку мы удалили и заменили сбойный диск(рис. [-@fig:011]):

![Состояние массива](image/11.png){#fig:011 width=70%}

Удалим массив и очистим метаданные(рис. [-@fig:012]):

![Удаление массива](image/12.png){#fig:012 width=70%}

Создадим новый массив и добавим к нему третий диск(рис. [-@fig:013]):

![Создание массива и добавление диска](image/13.png){#fig:013 width=70%}

Подмонтируем массив, и проверим его состояние. Как можно увидеть, всего три устройства в массиве, однако активных лишь два, а третий диск находится в запасе(рис. [-@fig:014]):

![Состояние массива](image/14.png){#fig:014 width=70%}	

Сымитируем сбой одного из дисков, после чего проверим состояние массива. Диск-запаска встал на место сбойного диска, и таким образом массив продолжил работать. По информации в массиве все также три устройства, но одно сбойное(рис. [-@fig:015]):

![Состояние массива после сбоя диска](image/15.png){#fig:015 width=70%}

Удалим массив и очистим метаданные(рис. [-@fig:016]):

![Удаление массива](image/16.png){#fig:016 width=70%}	

Создадим новый массив RAID 1 и добавим к нему третий диск(рис. [-@fig:017]):

![Создание массива и добавление диска](image/17.png){#fig:017 width=70%}	

Подмонтируем массив и проверим его состояние. У массива всего три устройства, но так как при создании мы использовали только два, третий диск ушел в запас(рис. [-@fig:018]):

![Состояние массива](image/18.png){#fig:018 width=70%}	

Изменим тип массива на RAID 5 и проверим его состояние. Несмотря на то, что мы поменяли тип, активных устройств все равно два. Нужно сделать третий диск активным, ведь для RAID 5 минимально нужно три диска(рис. [-@fig:019]):

![Состояние массива после изменения типа](image/19.png){#fig:019 width=70%}	

Изменим количество дисков на 3 и проверим состояние массива. Теперь у нашего массива три активных диска и нет диска в запасе.(рис. [-@fig:020]):

![Состояние массива после изменения кол-ва дисков](image/20.png){#fig:020 width=70%}	

Удалим массив и очистим метаданные. Также закомментируем добавленную строку в fstab(рис. [-@fig:021]):

![Файл fstab](image/21.png){#fig:021 width=70%}			

# Контрольные вопросы

1. RAID - массив дисков, созданный для хранения определённых важных данных. Если один диск перестанет работать, другие диски будут хранить ту же информацию, и она не потеряется.
2. Существуют разные RAID, с 0 до 6, 10, 50 и 60.
3. RAID 0, RAID 1, RAID 5, RAID 6.


# Выводы

В этой лабораторной работе я научился работать с массивами RAID и освоился с утилитой mdadm.


