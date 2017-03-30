Рабочий процесс Git для разработчиков Yii 2
===========================================

Итак, вы хотите разрабатывать Yii? Хорошо! Но для того чтоб увеличить шанс принятия ваших изменений,
пожалуйста следуйте следующим шагам. Если вы новичок в git и github, вы можете сначала проверить
[github help](http://help.github.com/), [try git](https://try.github.com) или прочитать о
[внутренней модели данных git](http://nfarina.com/post/9868516270/git-is-simpler).

Подготовка вашего рабочего окружения
------------------------------------

Следующие шаги будут создавать рабочее окружение для Yii, которое вы можете использовать для работы над основным кодом
фреймворка. *Эти шаги будут нужны только в первый раз*.

### 1. [Форкаем](http://help.github.com/fork-a-repo/) репозиторий Yii на github и клонируйте ваш форк в ваше рабочее окружение.

```
git clone git@github.com:YOUR-GITHUB-USERNAME/yii2.git
```

Если у вас есть проблемы с настройкой GIT для работы с GitHub в Linux, или вы получаете ошибку похожую на "Permission Denied
(publickey)", тогда вы должны настроить ваш GIT по [этой инструкции](http://help.github.com/linux-set-up-git/)

### 2. Добавляем главный репозиторий Yii как дополнительный внешний git репозиторий называемый "upstream"

Перейдите в каталог, куда вы склонировали Yii, как правило "yii2". Затем введите следующую команду:

```
git remote add upstream git://github.com/yiisoft/yii2.git
```

### 3. Настройка тестовой среды

Следующие шаги не обязательны, если вы хотите работать только с переводом или документацией.

- выполните `composer update` для установки зависимостей (если [composer у вас установлен глобально](https://getcomposer.org/doc/00-intro.md#globally)).

> Note: Если вы видите такие ошибки, как `Problem 1 The requested package bower-asset/jquery could not be found in
> any version, there may be a typo in the package name.`, необходимо запустить `composer global require "fxp/composer-asset-plugin:^1.2.0"`

- выполните `php build/build dev/app basic` для клонирования базового приложения и установки его зависимостей.
  Эта команда установит сторонние пакеты composer обычным образом, но создаст ссылку с репозитория yii2 на только
  что загруженный репозиторий. Таким образом у вас будет только один экземпляр кода.

  При необходимости делаем тоже самое для приложения advanced: `php build/build dev/app advanced`.

  Данная команда также может быть использована для обновления зависимостей, внутри она использует `composer update`.

> Note: по умолчанию URL репозиториев git на GitHub работают через SSH. Чтобы использовать HTTPS, добавьте
> флаг `--useHttp` к команде `build`.

**Теперь у нас есть рабочая площадка для экспериментов с Yii 2.**

Следующие шаги не обязательны.

### Модульные тесты

Вы можете выполнить модульные тесты с помощью команды `phpunit` в корневой директории приложения. Если у вас phpunit
не установлен глобально, вы можете запустить `php vendor/bin/phpunit`.

Некоторые тесты требуют дополнительно установки и настройки баз данных. Вы можете создать `tests/data/config.local.php`
для переопределения настроек, которые определены в `tests/data/config.php`.

Вы можете ограничить тестирование группой тестов, с которой вы сейчас работаете, например запускать только тесты для
валидаторов и redis. Вы можете получить список доступных групп выполнив `phpunit --list-groups`.

### Расширения

Для работы над расширениями вы можете склонировать репозиторий расширения. Мы сделали команду, которая поможет вам
сделать это:

```
php build/build dev/ext <extension-name>
```

где `<extension-name>` это имя расширения, например `redis`.

Если вы хотите протестировать расширение в одном из шаблонов приложений, просто добавьте его в `composer.json`
приложения, например добавив `"yiisoft/yii2-redis": "~2.0.0"` в секцию `require` базового приложения.
Запустите `php build/build dev/app basic` для установки расширения и его зависимостей и создания символической
ссылки на `extensions/redis` так чтоб вы работали не папке вендорных пакетов composer, а напрямую в репозиторий yii2.

> Note: по умолчанию URL репозиториев git на GitHub работают через SSH. Чтобы использовать HTTPS, добавьте
> флаг `--useHttp` к команде `build`.

Работа над багами и новыми функциями
------------------------------------

Приготовив вашу среду разработки вы можете начать работу над исправлением багов и разработкой новых функций.

### 1. Убедитесь, что issue создана для того, над чем вы работаете, если потребуется много времени для исправления

Все новые функции и баги должны быть связаны с issue для того, чтоб иметь единое место для обсуждения и документирования.
Потратьте несколько минут на поиск существующей issue, которая соответствует вашим изменениям. Если вы найдёте её в
списке, то пожалуйста оставьте комментарий, что вы начали над ней работать. Если вы не нашли нужной issue пожалуйста
[создайте новую issue](report-an-issue.md) или создайте сразу запрос на изменения если это простые изменения.
Это позволит команде проверить ваше предложение, и обеспечивать соответствующую обратную связь.

> Для небольших изменений или документации, или простых исправлений, вам нет необходимости создавать issue,
  запрос на изменения в этом случае подходит лучше.

### 2. Вытягивание последнего кода из основного репозитория Yii

```
git fetch upstream
```

Вы должны начинать с этого действия работу над каждым новым предложением, убеждайтесь что вы работаете над самой
последней версией кода.

### 3. Создание новой ветки для ваших изменений, основанных на текущем мастере Yii

> Это очень важно, так как вы не сможете отправлять более одного запроса на изменения из вашего репозитория, если
  будете использовать ветку master.

Каждое отдельное исправление или изменение должно разрабатываться в своей ветке. Имя ветки должно быть описательным
и начинаться с номера issue, с которым связан ваш код. Если вы не исправляете какой-то конкретный issue, просто
пропустите номер.
Например:

```
git checkout upstream/master
git checkout -b 999-name-of-your-branch-goes-here
```

### 4. Делайте свою магию, пишите ваш код

Убедитесь, что он работает :)

Модульные тесты всегда приветствуются. Протестированный и с хорошим покрытием код значительно упрощает задачу проверки
вашего предложения. Сломанные модульные тесты, как описание проблемы, тоже приветствуются.

### 5. Обновите CHANGELOG

Отредактируйте файл CHANGELOG, включив ваши изменения. Для этого нужно вставить строки в начало файла под заголовком
"Work in progress", строки с описанием изменений должны выглядеть похожими на следующие:

```
Bug #999: a description of the bug fix (Your Name)
Enh #999: a description of the enhancement (Your Name)
```

`#999` это номер issue описывающей `Bug` или `Enh`.
Лог изменений должен быть сгруппирован по типу (`Bug`,`Enh`) и отсортирован по номеру issue.

Для очень маленьких исправлений, например опечаток и изменений документации, нет необходимости обновлять CHANGELOG.

### 6. Фиксация ваших изменений

Добавляем файлы/изменения которые вы хотите зафиксировать в [staging area](http://gitref.org/basic/#add)

```
git add path/to/my/file.php
```

Вы можете использовать опцию `-p` для того, чтоб выбрать, какие изменения вы хотите добавить в коммит.

Фиксируйте ваши изменения с описательным сообщением. Убедитесь что в сообщение есть номер `#XXX`, так github
автоматически свяжет ваш коммит с тикетом:

```
git commit -m "A brief description of this change which fixes #999 goes here"
```

### 7. Получение последнего кода из апстрима Yii в вашу ветку

```
git pull upstream master
```

Это гарантирует, что вы используете самый последний код в вашей ветке перед отправкой запроса на изменения. Если есть
какие-либо конфликты слияния, вы должны исправить их и зафиксировать изменения ещё раз. Это гарантирует, что команда Yii
сможет слить ваши изменения одним кликом.

### 8. Разрешив зависимости, отправляем код на github

```
git push -u origin 999-name-of-your-branch-goes-here
```

Опция `-u` сохранит указание на ветку в github, чтобы при следующем выполнении `git push`, git знал, куда отправлять
изменения. Это полезно, если вы хотите позже отправлять ещё коммиты в этот запрос на слияние.

### 9. Открываем [запрос на слияние](http://help.github.com/send-pull-requests/) в *upstream*.

Перейдите в репозиторий на github и нажмите "Pull Request", выберите ветку справа и введите больше информации
в поле комментариев. Чтобы связать запрос на изменение с issue, добавьте в комментарий `#999` - где 999 это номер issue.

> Обратите внимание, что каждый запрос на слияние должен исправлять единственное изменение. Для множества независимых
  изменений, пожалуйста откройте несколько запросов на слияние.

### 10. Проверка вашего кода кем-то

Кто-то будет проверять ваш код, и, возможно, вам будет предложено внести некоторые изменения, если это так, то перейдите
к шагу #6 (вам не надо открывать новый запрос на слияние, если текущий ещё открыт). Если код будет принят, он будет
влит в основную ветку и станет частью следующего релиза Yii. Если нет, не унывайте, разным людям необходимы различные
функции и Yii не может реализовывать всё для всех, ваш код будет ещё доступен на github как ссылка для людей кому он
может пригодится.

### 11. Очистка

После того, как код был принят или отклонён, вы можете удалить ветки, над которыми вы работали в локальном репозитории
и в `origin`.

```
git checkout master
git branch -D 999-name-of-your-branch-goes-here
git push origin --delete 999-name-of-your-branch-goes-here
```

### Примечание

Для обнаружения регрессии как можно раньше, каждое слияние кодовой базы Yii на github будет подхвачено
[Travis CI](http://travis-ci.org) для автоматического запуска тестов. Люди из *core team* не хотят нагружать
этот сервис, поэтому добавляют текст [`[ci skip]`](http://about.travis-ci.org/docs/user/how-to-skip-a-build/) в описание
запроса на слияние, в следующих ситуациях:

* затронуты только javascript, css файлы или файлы изображений,
* обновление документации,
* изменения затрагивают только строки (например обновление переводов).

Это защитит travis от запуска тестов на изменениях, которые не покрыты тестами.

### Обзор команд (для продвинутых участников)

```
git clone git@github.com:YOUR-GITHUB-USERNAME/yii2.git
git remote add upstream git://github.com/yiisoft/yii2.git
```

```
git fetch upstream
git checkout upstream/master
git checkout -b 999-name-of-your-branch-goes-here

/* ваша магия, обновление changelog если нужно */

git add path/to/my/file.php
git commit -m "A brief description of this change which fixes #999 goes here"
git pull upstream master
git push -u origin 999-name-of-your-branch-goes-here
```