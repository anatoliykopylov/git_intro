# Полезные практики Git Commit

Оригинал: https://github.com/RomuloOliveira/commit-messages-guide/blob/master/README_ru-RU.md

## 1. Используйте повелительное наклонение

###### # Хорошо

`Use InventoryBackendPool to retrieve inventory backend`

###### # Плохо

`Used InventoryBackendPool to retrieve inventory backend`


## 2. Начинайте сообщение коммита с заглавной буквы
###### # Хорошо

`Add `use` method to Credit model`

###### # Плохо

`add `use` method to Credit model`


## 3. Старайтесь описывать изменения так, чтобы указывать на исходный код
###### # Хорошо

`Add `use` method to Credit model`

###### # Плохо

`Add `use` method`

###### # Хорошо

`Increase left padding between textbox and layout frame`

###### # Плохо

`Adjust css`


## 4. Используйте тело сообщения для объяснения "почему", "для чего", "как" и дополнительные детали

###### # Хорошо

`Fix method name of InventoryBackend child classes`

`Classes derived from InventoryBackend were not respecting the base class interface.`

`It worked because the cart was calling the backend implementation incorrectly.`

###### # Хорошо

`Serialize and deserialize credits to json in Cart`

`Convert the Credit instances to dict for two main reasons:`

  `- Pickle relies on file path for classes and we do not want to break up everything if a refactor is needed`
  `- Dict and built-in types are pickleable by default`

###### # Хорошо

`Add `use` method to Credit`

`Change from namedtuple to class because we need to setup a new attribute (in_use_amount) with a new value`


## 5. Избегайте общих сообщений или сообщений без какого-либо контекста

###### # Плохо

`Fix this`

`Fix stuff`

`It should work now`

`Change stuff`

`Adjust css`


## 6. Ограничьте длину строк

Рекомендуется использовать максимум 50 символов для темы и 72 символа для описания.


## 7. Сохраняйте согласованность языка

Для владельцев проектов: Выберите язык и пишите все сообщения коммитов используя этот язык. В идеале, он должен совпадать с комментариями в коде, стандартным переводом (для переведенных проектов), и т.д.


# Держите свою ветку в чистоте с помощью fixup и autosquash

https://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html

## Пример
Возьмите репозиторий git с веткой dev . Вы намерены зафиксировать функции A и B:


`$  ( dev ) git add featureA`

 `$  ( dev ) git commit -m «Функция A выполнена» `

`[dev fb2f677] Функция A выполнена `

`$  ( dev ) git add featureB`

 `$  ( dev ) git commit -m «Функция B выполнена» `

`[dev 733e2ff] Функция B готова`

Ваша работа продолжается, и вы нашли небольшие ошибки в функции A: пришло время использовать опцию --fixup !

`$  ( dev ) git add featureA` 

`$  ( dev ) git commit --fixup fb2f677`

` [dev c5069d5] fixup! Функция А выполнена`

Здесь вы видите, что GIT автоматически извлек сообщение фиксации featureA с префиксом fixup!.

Вся работа сделана, смотрим лог:

`$  ( dev ) git log --oneline`

` c5069d5 исправление! Функция A выполнена `

`733e2ff Функция B выполнена `

`fb2f677 Функция A выполнена `

`ac5db87 Предыдущая фиксация`

Теперь вы хотите очистить свою ветку перед ее слиянием: пришло время использовать опцию --autosquash !

`$  ( dev ) git rebase -i --autosquash ac5db87`

` pick fb2f677 Feature A is done `

`fixup c5069d5 fixup! Функция A выполнена. `

`pick 733e2ff Feature B is done. `

Эта команда открыла ваш редактор строками выше. Просто сохраните и выйдите и ... :

`$  ( dev ) git log --oneline`

` ff4de2a Функция B выполнена `

`5478cee Функция A выполнена `

`ac5db87 Предыдущая фиксация`


# cherry-pick

Эта команда может быть очень полезной для применения коммита, который был сделан в неверной ветке, чтобы не писать код заново.

Пример:

`$ git cherry-pick 790ab21`

`[master 094d820] Fix English grammar in Contributing`
` Date: Sun Feb 25 23:14:23 2018 -0300`
` 1 file changed, 1 insertion(+), 1 deletion(-)`


# git log

##  Наиболее распространённые опции для команды git log

`-p`

Показывает патч для каждого коммита.

`--stat`

Показывает статистику изменённых файлов для каждого коммита.

`--shortstat`

Отображает только строку с количеством изменений/вставок/удалений для команды --stat.

`--name-only`

Показывает список изменённых файлов после информации о коммите.

`--name-status`

Показывает список файлов, которые добавлены/изменены/удалены.

`--abbrev-commit`

Показывает только несколько символов SHA-1 чек-суммы вместо всех 40.

`--relative-date`

Отображает дату в относительном формате (например, «2 weeks ago») вместо стандартного формата даты.

`--graph`

Отображает ASCII граф с ветвлениями и историей слияний.

`--pretty`

Показывает коммиты в альтернативном формате. Возможные варианты опций: oneline, short, full, fuller и format (с помощью последней можно указать свой формат).

`--oneline`

Сокращение для одновременного использования опций --pretty=oneline --abbrev-commit.


## Опции для ограничения вывода команды git log
`-(n)`

Показывает только последние n коммитов.

`--since, --after`

Показывает только те коммиты, которые были сделаны после указанной даты.

`--until, --before`

Показывает только те коммиты, которые были сделаны до указанной даты.

`--author`

Показывает только те коммиты, в которых запись author совпадает с указанной строкой.

`--committer`

Показывает только те коммиты, в которых запись committer совпадает с указанной строкой.

`--grep`

Показывает только коммиты, сообщение которых содержит указанную строку.

`-S`

Показывает только коммиты, в которых изменение в коде повлекло за собой добавление или удаление указанной строки.