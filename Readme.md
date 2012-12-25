﻿Данный проект ставит целью собрание наиболее полной библиографии по историческим танцам. База данных хранится в формате `.bib` и предполагает интеграцию с пакетами обработки языка разметки LaTeX.

Обработка библиографической базы данных в LaTex выполняется двумя программами: фронтэндом (на стороне LaTeX) и бэкэндом (именно бэкэнд считывает базу данных и преобразует её в формат, понятный LaTeX'у). Теоретически, можно использовать любую существующую связку (фронтэнд + бэкэнд), официально поддерживаются две: `(natbib + bibtex8)` и `(biblatex + biber)`. Про них будет рассказано ниже. Кроме базы данных, реализованы собственные стилевые файлы для официально поддерживаемых связок (фронтэнд + бэкэнд).

## (natbib + bibtex8):

Требует наличия пакетов `natbib` и `bibtex8` (как правило, входят в стандартную установку дистрибутива, в противном случае легко устанавливаются из стандартных репозиториев). Подключение библиографии производится следующей командой:

	\newcommand{\rootfolder}{%folderpath%}
	\usepackage[root=\rootfolder]{\rootfolder/dancebooks-bibtex}

Здесь `%folderpath%` - путь к папке с библиографией (обратные слеши нужно заменить на прямые для корректной работы). В этой путь не должно быть последнего слэша.

Неправильно:

	D:\georg\dancebooks-bibtex
	D:/georg/dancebooks-bibtex/

Правильно:

	D:/georg/dancebooks-bibtex

После подключения пакета становятся доступны макросы цитирования `\cite{id}`, `\footcite{id}`, `\parencite{id}`, `\nocite{id}` и макрос печати библиографии `\printbibliography` с одним опциональным параметром, позволяющим перечислить дополнительный библиографические источники (.bib-файлы) через запятую без указания расширения (расширение `.bib` будет подставлено автоматически).
Пример использования:

	\printbibliography{hello,extra,file}

## (biblatex + biber):

С использованием этих пакетов дело обстоит несколько сложнее. Нужно установить biblatex, biblatex-gost и biber (про установку данных пакетов можно будет прочесть ниже. Стилевой файл подключается аналогично:

	\newcommand{\rootfolder}{%folderpath%}
	\usepackage[root=\rootfolder]{\rootfolder/dancebooks-biblatex}

После подключения становятся доступны макросы цитирования `\cite{id}`, `\footcite{id}`, `\parencite{id}`, `\nocite{id}`. Стандартный макрос печати библиографии в `biblatex` -- `\printbibliography`, без параметров. Дополнительные библиографические источники можно добавить стандартной командой `\addbibresource{hello.bib}` (расширение `.bib` необходимо указывать явно).

### Установка допольнительных пакетов. `biblatex`:

Скачать можно [по этому адресу](http://sourceforge.net/projects/biblatex/files/).

В MiKTeX 2.9 пакет есть в стандартном репозитории.

### Установка допольнительных пакетов. `biber`:

Скачать последнюю версию бэкэнда можно [по этому адресу](http://sourceforge.net/projects/biblatex-biber/files/biblatex-biber/).

Необходимо положить исполняемый файл в любую папку, после чего добавить эту папку в %PATH%, если этого не было сделано раньше.

Для x86-дистрибутивов пакет есть в стандартном репозитории (для MiKTeX он называется `miktex-biber-bin`).

### Установка допольнительных пакетов. `biblatex-gost`:

Скачать последнюю версию гостовских стилей можно [по этому адресу](http://sourceforge.net/projects/biblatexgost/files/).

Скачанный архив нужно распаковать (с сохранением структуры директорий) в любую из корневых папок вашего дистрибутива.

После установки пакета нужно выполнить команду обновления кэша (команда зависит от вашего дистрибутива, для MiKTeX -- `"initexmf -u"`).