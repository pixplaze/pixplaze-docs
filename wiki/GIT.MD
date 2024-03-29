# ШПАРГАЛКА ПО GIT

\* не одобрено Фиг знает Как Надо (ФКН) © корпорейтед

## Введение

### Терминология

Для начала работы, необходимо уяснить несколько терминов:

* *Git репозиторий* - директория (папка), находящаяся на локальной
или удалённой машине, подверженая управлению системой контроля версий Git.

* *Состояние файла* - что из себя представляет файл или папка в заданный момент времени.

* *Отслеживаемость (tracking)* - свойство файла, показывающее, следит ли Git за состоянием файла.

* *Изменённость (modification)* - свойство файла, показывающее был ли изменён файл по сравнению с предыдущим его состоянием

* *Индексируемость (indexing)* - свойство файла, показывающее готовность файла к фиксации его нового состояния.

* *Коммит (commit)* - снимок, зафиксированное состояние файла, а так же действие по его фиксации.

* *Ветка (branch)* - независимая история (последовательность) снимков. Другими словами - история действий.

* *Ветвление (fork)* - Группа нескольких веток и управление ими. Грубо говоря - дерево
независимых историй. Если веток в дереве несколько, то изменения состояния файлов и их
снимков в одной ветке, никак не влияют на состояния файлов и их снимков в другой ветке.

* *Слияние (migration)* - слияние в одну двух независимых историй (веток).



### Управление файлами в Git

#### Свойства файлов для Git

Система контроля версий Git может следить за изменением состояния файлов. 
Каждый файл для системы Git имеет три свойства: отслеживаемость, изменённость и индексируемость.


**Отслеживаемость** 	- свойство отслеживаемости означает, отслеживается ли вообще файл системой контроля версий Git;

**Изменённость** 	- свойство изменённости означает, был ли изменён *отслеживаемый* файл по сравнению с его предыдущим зафиксированным состоянием (коммитом).

**Индексируремость** 	- свойство индексируемости означает, будет ли *отслеживаемый*, *изменённый* файл зафиксирован при следующем сохранении его состояния (при следующем коммите).
Если файл индексируемый - значит файл готов к фиксации и его текущее состояние будет зафиксировано.
Если файл неиндексируемый, - значит файл к фиксации его состояния не готов и его состояние не будет зафиксировано.

> Индексируемость файла выделяется соответствующим цветом: красный - не индексируется, зелёный - индексируется.
> Индексируемость файла изменяется каждый цикл фиксации. Каждый коммит сбрасывает индексируемость.

Итак, файл может быть *отслеживаемым или не отслеживаемым*, *изменённым или не изменённым*, *индексируемым и неиндексируемым*.
Также каждый отслеживаемый файл имеет статус, список которых обозначен ниже.


#### Статусы файлов для Git

Git различает файлы по нескольким статусам:

* *Неотслеживаемый (Untracked)* - неотслеживаемый файл, - файл который не отслеживается системой контроля версий.

* *Неизменённый (Unmodified)* - отслеживаемый неизменённый, - файл, который был замечен системой как **пока неизменённый** (по сравнению с предыдущим зафиксированным состоянием).

* *Изменённый (Modified)* - отслеживаемый изменённый, - файл, который был замечен системой как **уже изменённый** (по сравнению с предыдущим зафиксированным состоянием).

* *Индексируемый (Staged)* - отслеживаемый, изменённый, индексируемый, - файл, который  был замечен системой как **уже изменённый** и **готовый к фиксации** его нового состояния.


**Важно!**

> Следует отметить, что отслеживаемые файлы, не обязательно будут зафиксированы в будущих снимках. Этот факт определяет статус готовности к фиксации *(индексируемость)*.
> Типы файлов имеют следующие статусы (согласно вышеописанному):
> 
> `Untracked` 	- не отслеживается, и как следствие не может быть проиндексирован;							\
> `Unmodified` 	- отслеживается, но не будет индексироваться, до тех пор пока не изменит свой статус на `Modified`;			\
> `Modified` 	- отслеживается, и может быть проиндексирован (свойство индексируемости изменяется командой: `git add <file>`);										\
> `Staged` 	- отслеживается, индексируется, как следствие - готов к фиксации.			


## Начало работы

### Установка

Предположим что Git уже установлен

### Создание Git репозитория

Создание Git репозитория подразумевает создание директории с файлами, состоянием которых управляет система контроля версий Git
и может производиться несколькими способами, в зависимости от целей:

* **Клонирование** репозитория с удалённой машины на локальную, в случае если мы хотим
получить чужой проект (директорию) с необходимыми нам файлами на нашу локальную машину.

* **Инициализация** нового репозитория в существующей директории, в случае если мы хотим создать свой
проект (директорию) под управлением системы контроля версий.


#### Клонирование публичного репозитория

Всё что нам нужно сделать:

1. Открыть папку, в которую мы хотим поместить Git репозиторий:

	```
	$ cd <path>
	```

	**Где:** `<path>` - путь до целевой дериктории, в которой будет создана папка репозитория.


2. Клонировать Git репозиторий с удалённой машины или сервера:

	```
	$ git clone <url>
	```

	**Где:** `<url>` - ссылка на необходимый удалённый репозиторий.

В случае, если удалённый репозиторий имеет открытый доступ, пойдёт загрузка удалённого
репозитория на нашу локальную машину. Папка с репозиторием
автоматически создастся в указанной целевой директории.


#### Инициализация нового репозитория

1. Открыть папку, в которую мы хотим поместить Git репозиторий:

	```
	$ cd <path>
	```

	**Где:** `<path>` - путь до целевой дериктории, в которой будет создана папка репозитория.


2. Создаём новую папку в целевой директории, даём ей желаемое имя репозитория:

	```
	$ mkdir <repository>
	```
	
	**Где:** `<repository>` имя нового репозитория.

После этого создастся новая директория, которая будет корневой для нашего репозитория.

3. Переходим в папку будущего репозитория

	```
	$ cd <repository>
	```

4. Инициализируем репозиторий в корневом каталоге

	```
	$ git init
	```


#### Загрузка в удалённый репозиторий

1. Создаём локальный репозиторий (см. предыдущий раздел)



2. Создаём все необходимые файлы в нашем репозитории

3. Создаём и настраиваем файл `.gitignore`

4. Добавляем все файлы проекта в индексацию Git:
	
	```
	git add .
	```
5. Фиксируем состояние файлов:

	```
	git commit -m "first commit"
	```

6. Создаём удалённый репозиторий на Github

7. Связываем наш локальный и удалённый репозитории:

	```
	git remote add origin https://github.com/<username>/<repository>.git
	```

	**Где:** `<repository>` - имя нашего удалённого репозитория, `<username>` - имя профиля GitHub

8. Выгружаем файлы из нашего локального репозитория в удалённый:
	
	```
	git push -u origin <branch>
	```

	**Где:** `<branch>` - главная ветка наших репозиториев, **по умолчанию - *master***; \
	т.е.: `git push -u origin master`


# ШПАРГАЛКА ПО БАЗОВЫМ КОМАНДАМ GIT

## Работа с репозиториями

### Доступ к GitHub репозиторию по токену

#### Соединение локального репозитория с удалённым по токену

```
git remote add origin https://<token>@github.com/<username>/<repository>.git <folder>
```
`<token>` - токен удалённого репозитория, \
`<repository>` - имя удалённого репозитория, \
`<username>` - имя профиля GitHub.


#### Обновление токена локального репозитория

1. Проверяем настройки удалённого репозитория:
	```
	git remote -v
	```
2. Удаляем старую связь с удалённым репозиторием:
	```
	git remote remove origin
	```
3. Привязываем удалённый репозиторий с новым токеном к нашему локальному
	```
	git remote add origin https://<token>@github.com/<username>/<repository>.git <folder>
	```

	`<token>` - токен удалённого репозитория, \
	`<repository>` - имя удалённого репозитория, \
	`<username>` - имя профиля GitHub.
	
	
### Клонирование репозитория

#### Клонирование всего удалённого репозитория

Всё что нам нужно сделать:

1. Открыть папку, в которую мы хотим поместить Git репозиторий:

	```
	$ cd <path>
	```

	**Где:** `<path>` - путь до целевой дериктории, в которой будет создана папка репозитория.


2. Клонировать Git репозиторий с удалённой машины или сервера:

	```
	$ git clone <url> <dir>
	```

	**Где:** \
	`<url>` - ссылка на необходимый удалённый репозиторий.
	`<dir>` - папка, в которую будет клонирован репозиторий.
	> Если <dir> не указана, то папка с репозиторием будет создана в текущей рабочей директории
	> (== pwd, или то что указано в статусе терминала до знака `$` - для Linux, `>` для Windows).
	> Если <dir> будет указана как `.` (точка), то репозиторий будет создан в текущей рабочей директории
	> (файлы репозитория будут помещены в текущую рабочую директорию, без создания папки).
	> В остальных случаях значения <dir> будет создана подпапка c именем <dir> в текущей рабочей директории,
	> (если не указан абсолютный путь).

В случае, если удалённый репозиторий имеет открытый доступ, пойдёт загрузка удалённого
репозитория на нашу локальную машину. Папка с репозиторием
автоматически создастся в указанной целевой директории.


#### Клонирование одной ветки удалённого репозитория

```
git clone --branch <branch> https://github.com/<username>/<repository>.git <folder>
```

**Где:** \
`<branch>` - имя удалённой ветки, которую необходимо клонировать \
`<repository>` - имя удалённого репозитория, \
`<username>` - имя профиля GitHub, \
`<folder>` - путь к папке, в которую будут скопированы файлы репозитория.

> Если вместо `<folder>` указать `.` (точку), файлы будут скопированы в ту папку, из которой выполняется команда.
> Если `<folder>` не указывать, то в текущей директории (в которой выполняется команда) будет создана папка с
> файлами репозитория с таким же именем, как удалённый репозиторий.


## Работа с ветками

### Слияние веток


1. Переходим на ветку, в которую мы хотим добавить снимки (изменения)
	```
	git checkout <branch>
	```
	**Где:** `<branch>` - имя ветки, в которую мы хотим влить коммиты другой ветки.

2. Делаем слияние с другой веткой
	```
	git merge <branch>
	```
	**Где:** `<branch>` - имя ветки, из которой мы копируем историю снимков.

### Создание веток

#### Создани ветки

```
git branch <branch>
```

**Создание новой ветки и мгновенное перерключение на неё**
```
git checkout -b <branch>
```
**Где:** `<branch>` - имя новой ветки

### Удаление веток ...



## Работа с тегами ...
## Работа с коммитами ...
## Работа с историей

## Просмотр истории
### Просмотр истории ветки
```
git log
```
### Просмотр истории ветки в одну строку
```
git log --oneline
```


### Переход рабочего дерева к определённому коммиту:

```
git checkout <hash>
```
**Где:** `<hash>` - хеш коммита


### Переход рабочего дерева к определённому тегу:

```
git checkout <tag>
```
**Где:** `<hash>` - имя тега


## Отмена действий

### Перезапись последнего коммита

```
git commit --amend
```

Эта команда позволяет объединить проиндексированные изменения с предыдущим коммитом 
без создания нового коммита.
Лучше использовать эту команду, когда предыдущий коммит был сделан случайно
или с некоторыми ошибкам - допустим мы забыли добавить в коммит некоторые файлы
или хотим изменить комментарий (`git commit --amend -m "<comment>"`).


### Отмена индексации файла в коммите

**1. Вариант**
```
git restore --staged <file>
```

**2. Вариант**
```
git reset <file>
```

> Команда `restore` была введена в git с версии 2.23.0, и используется
как более удобная альтернатива команде `reset`.

Отмена индексации подразумевает, что файлы, для которых будет произведена
отмена индексации, не попадут в следующий коммит, даже если ранее они были добавлены в отслеживание.
Иными словами, если бы мы вовсе не добавляли их к отслежениванию командой `git add`.

Это необходимо в том случае, когда мы передумали добавлять файл (изменения в файле) в новый коммит.


### Возврат к состоянию предыдущего коммита

```
git restore <file>
```

Данная команда позволяет вернуть файл к последнему коммиту.
Любые локальные изменения, внесенные в этот файл, исчезнут — Git просто
заменит файл последней зафиксированной версией.

**Внимание!**
> Важно понимать, что git restore <file> — опасная команда.
>
> Не следует использовать эту команду, если точно неизвестно,
> нужны ли эти несохраненные локальные изменения.