Оформлення основного коду фреймворку Yii 2
==========================================

Нижченаведений стиль кодування використовується у розробці основного коду Yii 2.x та офіційних розширень. Дотримуйтесь його,
якщо хочете вносити зміни в основний код. Команда розробників не наполягає на використанні цього стилю для вашого додатка.
Вільно обирайте те, що підходить вам більше.

Ви можете отримати конфігурацію для CodeSniffer за посиланням: https://github.com/yiisoft/yii2-coding-standards

1. Загальні положення
---------------------

В основному командою розробників використовується стиль сумісний з [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md),
тому все, що стосується
[PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md), застосовується також.

- У файлах НЕОБХІДНО використовувати теги або `<?php` або `<?=`.
- Пустий рядок у кінці файлу є необхідним.
- Файли з кодом PHP ПОВИННІ зберігатись лише у кодуванні UTF-8 без BOM.
- Для кожного рівня відступу НЕОБХІДНО використовувати 4 пробіли, а не табуляцію.
- Імена класів ПОВИННІ оголошуватись як `StudlyCaps`.
- Імена констант класу ПОВИННІ оголошуватись повністю у верхньому регістрі, підкреслення використовується як роздільник.
- Імена методів ПОВИННІ оголошуватись як `camelCase`.
- Імена властивостей ПОВИННІ оголошуватись як `camelCase`.
- Імена приватних властивостей ПОВИННІ починатись з підкреслення.
- Завжди використовуйте `elseif` замість `else if`.

2. Файли
--------

### 2.1. Теги PHP

- PHP код ПОВИНЕН використовувати теги `<?php ?>` або `<?=`; він НЕ ПОВИНЕН використовувати інші варіації, такі як `<?`.
- Якщо файл містить лише PHP він не повинен закінчуватись тегом `?>`.
- Не додавайте пробіли у кінці рядку.
- Будь-який файл, який містить код PHP, повинен мати розширення `.php`.

### 2.2. Кодування символів

PHP код ПОВИНЕН використовувати лише UTF-8 без BOM.

3. Імена класів
---------------

Імена класів ПОВИННІ оголошуватись як `StudlyCaps`. Наприклад: `Controller`, `Model`.

4. Класи
--------

Тут термін "клас" відноситься до всіх класів та інтерфейсів.

- Класи повинні іменуватись як `CamelCase`.
- Початкова фігурна дужка повинна завжди розміщуватись на наступному рядку після імені класу.
- Кожний клас повинен мати блок документації, який відповідає стандарту PHPDoc.
- Код всередині класу повинен бути зміщений на рівень відступу.
- Один PHP файл може містити лише один клас.
- Кожний клас повинен бути у просторі імен.
- Ім’я класу повинне відповідати імені файлу. Простір імен класу повинен відповідати структурі директорій.

```php
/**
 * Документація
 */
class MyClass extends \yii\Object implements MyInterface
{
    // код
}
```

### 4.1. Константи

Імена констант ПОВИННІ оголошуватись повністю у верхньому регістрі, підкреслення використовується як роздільник.
Наприклад:

```php
<?php
class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. Властивості

- При оголошенні публічних членів класу обов’язково вказуйте ключове слово `public`.
- Публічні та захищені змінні повинні бути оголошенні у початку класу перед будь-яким оголошенням методу.
  Приватні змінні також повинні бути оголошенні у початку класу, але можуть бути вставленні безпосередньо перед методами,
  що ними оперують, у випадках коли змінні пов’язані лише з невеликою кількістю методів класу.
- Порядок оголошення властивостей у класі повинен бути таким: спочатку публічні, потім захищені, а потім приватні.
- Для кращої читабельності не повинно бути пустих рядків між оголошеннями властивостей та повинно бути два пустих рядки
  між секціями оголошення властивості та методу.
- Приватні змінні повинні іменуватись як `$_varName`.
- Публічні члени класу та автономні змінні повинні іменуватись як `$camelCase`
  (перша літера у нижньому регістрі).
- Використовуйте описові імена. Змінні, такі як `$i` та `$j`, краще не використовувати.

Наприклад:

```php
<?php
class Foo
{
    public $publicProp;
    protected $protectedProp;
    private $_privateProp;
}
```

### 4.3. Методи

- Функції та методи повинні іменуватись як `camelCase` (перша літера у нижньому регістрі).
- Ім’я повинне бути само-описовим та вказувати призначення функції.
- Методи класу завжди повинні оголошувати видимість, використовуючи модифікатори `private`, `protected` та
  `public`. Не допускається використання `var`.
- Початкова фігурна дужка функції повинна розміщуватись на наступному рядку після оголошення функції.

```
/**
 * Документація
 */
class Foo
{
    /**
     * Документація
     */
    public function bar()
    {
        // код
        return $value;
    }
}
```

### 4.4 Блоки документації PHPDoc (Doc-блоки)

`@param`, `@var`, `@property` та `@return` повинні оголошувати типи як `bool`, `int`, `string`, `array` чи `null`. Також можна використовувати імена класів, як наприклад: `Model` або `ActiveRecord`. Для типізованих масивів використовуйте `ClassName[]`.

### 4.5 Конструктори

- потрібно використовувати `__construct` замість стилю конструкторів PHP 4.

## 5 PHP

### 5.1 Типи

- Усі типи PHP та значення повинні бути у нижньому регістрі. Це включає `true`, `false`, `null` та `array`.

Зміна типу змінної, що вже існує, вважається поганою практикою. Намагайтесь не писати такий код, поки в цьому дійсно нема потреби.


```php
public function save(Transaction $transaction, $argument2 = 100)
{
    $transaction = new Connection; // погано
    $argument2 = 200; // добре
}
```

### 5.2 Текстові рядки

- Якщо текстовий рядок не містить змінних чи одинарних лапок, використовуйте одинарні лапки.

```php
$str = 'Текстовий рядок.';
```

- Якщо текстовий рядок містить одинарні лапки, можна використовувати подвійні лапки, щоб уникнути додаткового екранування символів.

#### Підставлення змінної

```php
$str1 = "Привіт, $username!";
$str2 = "Привіт, {$username}!";
```

Нижченаведений приклад не допускається:

```php
$str3 = "Привіт, ${username}!";
```

#### Конкатенація

Додавайте пробіли навколо оператора конкатенації (.), коли об’єднуєте текстові рядки:

```php
$name = 'Фреймворк ' . 'Yii';
```

Для довгих текстових рядків використовуйте наступний формат:

```php
$sql = "SELECT *"
    . "FROM `post` "
    . "WHERE `id` = 121 ";
```

### 5.3 Масиви

Для масивів використовуйте скорочений синтаксис (PHP 5.4).

#### Індексовані масиви

- Не використовуйте від’ємні числа для індексів масиву.

Використовуйте нижченаведений формат оголошення масиву:

```php
$arr = [3, 14, 15, 'Yii', 'фреймворк'];
```

Якщо забагато елементів для одного рядка:

```php
$arr = [
    3, 14, 15,
    92, 6, $test,
    'Yii', 'фреймворк',
];
```

#### Асоціативні масиви

Використовуйте нижченаведений формат для асоціативних масивів:

```php
$config = [
    'name'  => 'Yii',
    'options' => ['usePHP' => true],
];
```

### 5.4 Керування порядком виконання

- Перед умовою керувальної інструкції та після неї повинен бути пробіл.
- Оператори всередині круглих дужок повинні відокремлюватись пробілами.
- Початкова фігурна дужка розміщена на тому самому рядку.
- Кінцева фігурна дужка розміщена на новому рядку.
- Завжди використовуйте фігурні дужки для конструкцій з одного рядка.

```php
if ($event === null) {
    return new Event();
}
if ($event instanceof CoolEvent) {
    return $event->instance();
}
return null;


// нижченаведений приклад НЕ допускається:
if (!$model && null === $event)
    throw new Exception('test');
```

Краще уникайте використання `else` після `return`, де це має сенс.
Використовуйте [вартові умови](http://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html).

```php
$result = $this->getResult();
if (empty($result)) {
  return true;
} else {
  // обробка результату
}
```

буде краще так:

```php
$result = $this->getResult();
if (empty($result)) {
  return true;
}

// обробка результату
```

#### switch

Використовуйте наступний формат для switch:

```php
switch ($this->phpType) {
    case 'string':
        $a = (string) $value;
        break;
    case 'integer':
    case 'int':
        $a = (int) $value;
        break;
    case 'boolean':
        $a = (bool) $value;
        break;
    default:
        $a = null;
}
```

### 5.5 Виклики функції

```php
doIt(2, 3);

doIt(['a' => 'b']);

doIt('a', [
    'a' => 'b',
    'c' => 'd',
]);
```

### 5.6 Оголошення анонімних (лямбда) функцій

Зверніть увагу на пробіл між `function`/`use` та початковою круглою дужкою:

```php
// добре
$n = 100;
$sum = array_reduce($numbers, function ($r, $x) use ($n) {
    $this->doMagic();
    $r += $x * $n;
    return $r;
});

// погано
$n = 100;
$mul = array_reduce($numbers, function($r, $x) use($n) {
    $this->doMagic();
    $r *= $x * $n;
    return $r;
});
```

Документація
------------

- Див. [PHPDoc](http://phpdoc.org/) для довідки про синтаксис документації.
- Код без документації не допускається.
- Усі файли класів повинні містити файловий ("file-level") doc-блок на початку
  та класовий ("class-level") doc-блок безпосередньо над кожним класом.
- Нема потреби використовувати `@return`, якщо метод нічого не повертає.
- Усі віртуальні властивості у класах успадкованих від `yii\base\Object`
  документуються з тегом `@property` у класовому doc-блоці.
  Ці анотації генеруються автоматично із тегів `@return` чи `@param`
  відповідних геттерів або сеттерів виконанням команди `./build php-doc` у директорії build.
  Ви можете додати тег `@property`
  до геттеру або сеттеру, щоб точно визначити повідомлення для документації властивості,
  яка представляється цими методами, коли опис відрізняється від того, що встановлено
  тегом `@return`. Наприклад:

  ```php
    <?php
    /**
     * Returns the errors for all attributes or a single attribute.
     * @param string $attribute attribute name. Use `null` to retrieve errors for all attributes.
     * @property array An array of errors for all attributes. Empty array is returned if no error.
     * The result is a two-dimensional array. See [[getErrors()]] for detailed description.
     * @return array errors for all attributes or the specified attribute. Empty array is returned if no error.
     * Note that when returning errors for all attributes, the result is a two-dimensional array, like the following:
     * ...
     */
    public function getErrors($attribute = null)
  ```

#### Файл

```php
<?php
/**
 * @link http://www.yiiframework.com/
 * @copyright Copyright (c) 2008 Yii Software LLC
 * @license http://www.yiiframework.com/license/
 */
```

#### Клас

```php
/**
 * Component is the base class that provides the *property*, *event* and *behavior* features.
 *
 * @include @yii/docs/base-Component.md
 *
 * @author Qiang Xue <qiang.xue@gmail.com>
 * @since 2.0
 */
class Component extends \yii\base\Object
```


#### Функція / метод

```php
/**
 * Returns the list of attached event handlers for an event.
 * You may manipulate the returned [[Vector]] object by adding or removing handlers.
 * For example,
 *
 * ```
 * $component->getEventHandlers($eventName)->insertAt(0, $eventHandler);
 * ```
 *
 * @param string $name the event name
 * @return Vector list of attached event handlers for the event
 * @throws Exception if the event is not defined
 */
public function getEventHandlers($name)
{
    if (!isset($this->_e[$name])) {
        $this->_e[$name] = new Vector;
    }
    $this->ensureBehaviors();
    return $this->_e[$name];
}
```

#### Markdown

Як ви могли побачити у прикладах вище, для форматування коментарів PHPDoc використовується markdown.

Існує додатковий синтаксис для створення перехресних посилань між класами, методами та властивостями у документації:

- `[[canSetProperty]]` створить посилання на метод або властивість `canSetProperty` того ж самого класу.
- `[[Component::canSetProperty]]` створить посилання на метод `canSetProperty` класу `Component` в тому ж самому просторі імен.
- `[[yii\base\Component::canSetProperty]]` створить посилання на метод `canSetProperty` класу `Component` з простору імен `yii\base`.
- `[[Component]]` створить посилання на клас `Component` в тому ж самому просторі імен. Додавання простору імен до імені класу тут також можливе.

Щоб для одного з вище зазначених посилань вказати мітку відмінну від імені класу чи методу, ви можете використовувати синтаксис, показаний в нижченаведеному прикладі:

```
... as displayed in the [[header|header cell]].
```

Частина перед | є найменуванням методу, властивості або класу, в той час як частина після | є міткою посилання.

Також можливо посилатись на Посібник, використовуючи наступний синтаксис:

```markdown
[link to guide](guide:file-name.md)
[link to guide](guide:file-name.md#subsection)
```


#### Коментарі

- Одно-рядкові коментарі повинні починатись з `//`, а не з `#`.
- Одно-рядковий коментар повинен бути розміщений на власному рядку.

Додаткові правила
-----------------

### `=== []` проти `empty()`

Використовуйте `empty()`, де можливо.

### Кілька інструкцій return

При великій вкладеності умов, використовуйте інструкцію return раніше. Якщо метод не великий, це неважливо.

### `self` проти `static`

Завжди використовуйте `static`, за виключенням наведених випадків:

- отримання значень констант ПОВИННО виконуватись через `self`: `self::MY_CONSTANT`
- отримання значень приватних статичних властивостей ПОВИННО виконуватись через `self`: `self::$_events`
- Дозволено використовувати `self` для рекурсії, щоб викликати поточне втілення знову замість розширення реалізації класу.

### Значення для "не робити чогось"

Властивості, яким дозволено сконфігурувати компонент не робити чогось, повинні приймати значення `false`. Значення `null`, `''` чи `[]` не повинні вважатись такими.

### Імена директорій та просторів імен

- використовуйте нижній регістр
- використовуйте форму множини для іменників, які представляють об’єкти (наприклад, validators)
- використовуйте форму однини для імен, які представляють відповідну функціональність/можливості (наприклад, web)