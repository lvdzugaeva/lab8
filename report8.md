---
# Front matter
title: "Отчёт по лабораторной работе"
subtitle: "Лабораторная работа 8"
author: "Дзугаева Лилия Владиславовна"

# Generic otions
lang: ru-RU

# Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

# Pdf output format
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
### Fonts
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
## Misc options
indent: true
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
  - \usepackage  # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

## Цель работы

Освоить на практике применение режима однократного гаммирования на примере кодирования различных исходных текстов одним ключом.

## Выполнение лабораторной работы

1.	Генерируем случайный ключ, соответствующий длине текста, который мы хотим кодировать. Вводим два сообщения. Применяя алгоритм, указанный в условии лабораторной работы, получаем, что можем расшифровать сообщения. Т.е. если злоумышленник знает одно из закодированных сообщений по одному ключу, то он сможет расшифровать и (уменьшить область поиска) другие сообщения, закодированные по тому же ключу.

![рис. 1.](image/1.jpg){ #fig:001 width=70% }


2. Ответы на контрольные вопросы:

	  1. _Как, зная один из текстов, определить другой, не зная при этом ключа?_
    С помощью формул режима однократного гаммирования получим шифротексты обеих телеграмм:
      C_1 =  P_1 ⊕ К
      C_2 =  P_2 ⊕ К.
    Задача нахождения открытого текста по известному шифротексту двух телеграмм, зашифрованных одним ключом, может быть решена. Складываем по модулю 2 (XOR) (обозначается знаком ) оба равенства и получаем:
      C_1 ⊕ C_2 = P_1 ⊕ К ⊕ P_2 ⊕ К = P_1 ⊕ P_2.
    Если один из текстов известен — т.е. имеет фиксированный формат, в который вписываются значения полей, и нам известен этот формат, то тогда получим достаточно много пар C_1 ⊕ C_2 (известен вид обеих шифровок). Далее зная P_1 и учитывая свойство операции XOR, имеем:
      C_1 ⊕ C_2 ⊕ P_1 = P_1 ⊕ P_2 ⊕ P_1 = P_2.
    Таким образом, получаем возможность определить те символы сообщения P_2, которые находятся на позициях известного шаблона сообщения P_1. В соответствии с логикой сообщения P_2, у нас есть реальный шанс узнать ещё некоторое количество символов сообщения P_2. Затем вновь используем предыдущее равенство с подстановкой вместо P_1 полученных на предыдущем шаге новых символов сообщения P_2. И так далее. Действуя подобным образом, даже если не прочитаем оба сообщения, то значительно уменьшим пространство их поиска.

	  2. _Что будет при повторном использовании ключа при шифровании текста?_
    Если на сообщение наложить ключ дважды, мы получим исходное сообщение.

	  3. _Как реализуется режим шифрования однократного гаммирования одним ключом двух открытых текстов?_
    Один ключ накладываем на оба открытых текста и получаем два зашифрованных одним ключом шифротекста.

	  4. _Перечислите недостатки шифрования одним ключом двух открытых текстов._
    При условии, что злоумышленник знает о том, что ключ шифрования един и он получил одну из пар текстов (зашифрованный текст и открытый), то он может найти ключ (см. вопрос 1) и расшифровать остальные тексты.

	  5. _Перечислите преимущества шифрования одним ключом двух открытых текстов._
    Это позволяет упростить разработку шифровальных и дешифровальных систем. Если мы реализуем обмен, например, между двумя компьютерами, то удобно использовать единый ключ для всех данных.


## Выводы

В ходе выполнения лабораторной работы я изучил теорию и освоил на практике применение режима однократного гаммирования на примере кодирования различных исходных текстов одним ключом.

# Список литературы{.unnumbered}

::: {#refs}
:::
