# Шаблоны для бакалаврского и магистерского дипломов

Здесь приведены годные шаблоны для оформления дипломов на кафедре космической физики МФТИ.

## Авторы

* Киселёв А. А.
* Долгоносов М. С.

## Системные требования

Очевидно, требуется установленный дистрибутив LaTeX. Пакет тестировался с TeX Live 2014 в GNU/Linux при сборке с pdflatex, но должен работать и с достаточно новыми версиями MikTeX на Windows. Предполагается, что в редакторе установлена кодировка UTF-8 (**это важно!**).

## Пример использования

Здесь приведен минимальный пример использования. При возникновении вопросов _обязательно_ прочтите следующие разделы.

`example.tex`

    \documentclass{mipt-thesis-bs}
    % Следующие две строки нужны только для biblatex. Для inline-библиографии их следует убрать.
    \usepackage{mipt-thesis-biblatex}
    \addbibresource{example.bib}

    \title{Изучение мохнатых существ с $\alpha$ Центавра}
    \author{Сидоров А.\,Б.}
    \supervisor{Иванов В.\,Г.}
    %\referee{Петров Д.\,Е.}       % требуется только для mipt-thesis-ms
    \groupnum{082}
    \faculty{Факультет проблем физики и энергетики}
    \department{Кафедра космической физики}

    \begin{document}

    \frontmatter
    \titlecontents

    \mainmatter


    \chapter{Введение}

    Здесь идет текст. Вот так выглядит ссылка на библиографию \cite{langmuir26}. Аналогично добавляются еще главы, внутри них можно объявлять секции с помощью \verb|\section|.


    \backmatter

    \printbib
    % Следующие строки необходимо раскомментировать, а предыдущую закомментировать, если используется inline-библиография.
    %\begin{thebibliography}{99}
    %    \bibitem{langmuir26}
    %        H. Mott-Smith, I. Langmuir. ``The theory of collectors in gaseous discharges''. \emph{Phys. Rev.} \textbf{28} (1926)
    %\end{thebibliography}

    \chapter{Благодарности}

    Благодарности идут тут.

    \end{document}

`example.bib`

    @article{langmuir26,
        author = "Mott-Smith, H. and Langmuir, I.",
        title = "The theory of collectors in gaseous discharges",
        journal = "Phys. Rev.",
        volume = "28",
        year = "1926",
        langid = "english"
    }


## Общие замечания

В пакете содержится два класса документа: `mipt-thesis-bs` для бакалаврского и `mipt-thesis-ms` для магистерского дипломов.  В нем учтены все основные требования по оформлению, включать какие-то дополнительные пакеты для корректной работы необязательно. Опционально, при использовании Biblatex, рекомендуется подключить стилевой файл `mipt-thesis-biblatex.sty`.

## Титульный лист и содержание

Для настройки титульного листа нужно вызвать макросы, определяющие название диплома (`\title`), имя автора (`\author`), имя научрука (`\supervisor`), номер группы (`\groupnum`), название факультета и кафедры (`\faculty` и `\department`) и, для магистерского диплома, имя рецензента (`\referee`). Далее для генерации надо вызвать макрос `\titlecontents`.

## Разделы и основной текст

Класс документа основан на классе `book`, поэтому настоятельно рекомендуется для основных частей использовать `\chapter`, а не `\section`.

С классом документа подгружаются многие полезные пакеты. Например, `esint` -- позволяет записывать интегралы по поверхности и объему при помощи `\oiint` и `\oiiint`, `siunitx` -- удобное использование единиц измерения, углов и больших чисел. Также включены все пакеты AMS и поддержка для индексов в формулах на русском языке.

Шаблон заточен на использование точки в качестве десятичного разделителя. Насколько мне известно, сейчас это стандарт де-факто в русской типографике. Если очень хочется использовать запятые, то рекомендуется загрузить пакет icomma, который выставит правильные отступы.

Для удобства оформления ссылок на рисунки и формулы есть макросы `\formref` (вместо `\ref` для формул) и `\picref` (вместо `\ref` для иллюстраций). Впрочем, обычный макрос `\ref` тоже доступен.

## Библиография

Для оформления библиографии можно использовать либо inline-способ, либо biblatex + biber. BibTeX не умеет работать с юникодом, так что он не рекомендуется вовсе к использованию.

### Inline-способ

В этом случае в конце документа (как раз перед `\end{document}`) пишется
следующее:

    \begin{thebibliography}{99}
    \bibitem{ivanov14}
        Иванов А. Б. <<Какая-то статья>>. \emph{Журнал каких-то наук}, 1.2 (2014)

    ...

    \end{thebibliography}

Недостаток этого метода -- оформление нужно делать вручную. Преимущество -- нет необходимости устанавливать biber.

### biblatex + biber (рекомендуемый)

В этом случае сначала надо установить biber и прописать его в настройках редактора LaTeX ([инструкция для texmaker в Windows](http://tex.stackexchange.com/questions/44040/biblatex-biber-texmaker-miktex#44095)). В командной строке GNU/Linux можно собрать при помощи команды вида `pdflatex example.tex && biber example && pdflatex example.tex`.

Преимущество такого метода -- проще использовать библиографию в нескольких статьях, не задумываясь о ручном оформлении. Недостаток -- необходимо настроить систему для работы с biber.

Библиография пишется в отдельном bib-файле (обычно с таким же названием, что и tex-файл). Обычно в редакторах есть шаблоны записей для biblatex/bibtex, но на всякий случай приведу примеры:

Статья в журнале:

    @article{langmuir26,
        author = "Mott-Smith, H. and Langmuir, I.",
        title = "The theory of collectors in gaseous discharges",
        journal = "Phys. Rev.",
        volume = "28",
        year = "1926",
        langid = "english"
    }

Глава из книги:

    @inbook{morse74,
        author = "Морз, Р.",
        title = "Бесстолкновительный PIC-метод",
        booktitle = "Вычислительные методы в физике плазмы",
        editor = "Олдера, Б. and Фернбаха, С. and Ротенберга, М.",
        publisher = "М.: Мир",
        year = 1974,
        langid = "russian"
    }

Выступление на конференции:

    @conference{kiselyov14_conf,
        author = "Киселёв, А. А. and Долгоносов М. С. and Красовский В. Л.",
        title = "Численное моделирование захвата ионов бесстолкновительной плазмы электрическим полем поглощающей сферы",
        booktitle = "Девятая ежегодная конференция <<Физика плазмы в Солнечной системе>>",
        year = 2014,
        langid = "russian"
    }
