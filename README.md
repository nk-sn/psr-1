# PSR-1: Основной стандарт кода

Данные правила является переводом на русский язык правил [PSR-1] от компании PHP Framework Interop Group.

Этот раздел стандарта содержит то, что следует считать стандартом элементов кода,
которые необходимы для обеспечения высокого уровня технической
совместимости между общим кодом PHP.  

Ключевые слова «ОБЯЗАН», «ОБЯЗАН НЕ», «ТРЕБУЕТСЯ», «ДОЛЖЕН», «ДОЛЖЕН НЕ», «СЛЕДУЕТ»,
«СЛЕДУЕТ НЕ», «РЕКОМЕНДУЕТСЯ», «МОЖЕТ» и «ПО ЖЕЛАНИЮ» в этом документе должны быть
интерпретируется, как описано в [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[BOM]: https://ru.wikipedia.org/wiki/Маркер_последовательности_байтов

## 1. Обзор
* Файлы ОБЯЗАНЫ использовать только теги `<?php` и `<?`.  
* Файлы ОБЯЗАНЫ использовать для кода PHP только UTF-8 без [BOM](https://ru.wikipedia.org/wiki/Маркер_последовательности_байтов).  
* Файлы ДОЛЖНЫ либо объявлять символы (классы, функции, константы и т.д.) или вызывать побочные эффекты (например, генерировать выходные данные, изменять настройки .ini и т.д.), но НЕ ДОЛЖНЫ делать и то и другое.  
* Пространства имен и классы ОБЯЗАНЫ следовать «автозагрузки» PSR: [[PSR-0], [PSR-4]].  
* Названия классов ОБЯЗАНЫ быть объявлены в `StudlyCaps`.  
* Константы класса ОБЯЗАНЫ быть объявлены в верхнем регистре с разделителями подчеркивания `CONSTANT` или `NEW_CONSTANT`.  
* Имена методов ОБЯЗАНЫ быть объявлены в `camelCase`.  

## 2. Файлы

### 2.1. PHP теги
PHP код ОБЯЗАН использовать длинные теги `<?php ?>` или короткие теги вывода `<?= ?>`; Файлы ОБЯЗАНЫ НЕ использовать другие варианты тегов.

### 2.2. Кодировка символов
PHP код ОБЯЗАН использовать только UTF-8 без [BOM].

### 2.3. Побочные эффекты

Файл ДОЛЖЕН объявлять новые символы (классы, функции, константы,
и т.д.) без вызова никаких побочных эффектов, или ДОЛЖЕН выполнять логику с побочными эффектами, но ДОЛЖЕН НЕ делать и то и другое.

Фраза «побочные эффекты» означает выполнение логики, не связанной непосредственно с объявлением классов, функций, констант и т.д., только из включаемого файла.

«Побочные эффекты» включают, но не ограничиваются: генерирование вывода, явное использование `require` или `include`, подключение к внешним службам, изменение настроек ini, генерирование ошибок или исключений, изменение глобальных или статических переменных, чтение или запись в файл и т.д.

Ниже приведен пример файла с объявлением и побочными эффектами; то есть пример того, чего следует избегать:
```php
<?php
// побочный эффект: изменение настроек ini
ini_set('error_reporting', E_ALL);

// побочный эффект: загрузка файла
include "file.php";

// побочный эффект: генерирование вывода
echo "<html>\n";

// объявление
function foo()
{
    // тело функции
}
```

Следующий пример представляет собой файл, содержащий объявления без побочных эффектов; то есть пример того, чему следует подражать:
```php
<?php
// объявление
function foo()
{
    // тело функции
}

// объявление с условием НЕ побочный эффект
if (! function_exists('bar')) {
    function bar()
    {
        // тело функции
    }
}
```

## 3. Пространства имен и имена классов

Пространства имен и классы ОБЯЗАНЫ следовать правилам «автозагрузки» PSR: [[PSR-0], [PSR-4]].

Это означает, что каждый класс находится в отдельном файле, и находится в пространстве имен хотя бы одного уровня: верхний уровень имя поставщика (vendor).

Названия классов ОБЯЗАНЫ быть объявлены в `StudlyCaps`.

Код, написанный для PHP 5.3 и выше ОБЯЗАН использовать формальные пространства имен.

Например:
```php
<?php
// PHP 5.3 и выше:
namespace Vendor\Model;

class Foo
{
}
```

Код, написанный для 5.2.x и ниже ДОЛЖЕН использовать соглашение о псевдо пространств имен, добавляя префикс `Vendor_` перед именами классов.
```php
<?php
// PHP 5.2.x и ниже:
class Vendor_Model_Foo
{
}
```
## 4. Константы, свойства и методы классов

### 4.1. Константы

Константы класса ОБЯЗАНЫ быть объявлены в верхнем регистре с разделителями подчеркивания.  
Например:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. Свойства

Это руководство преднамеренно избегает любых рекомендаций относительно использования
`$StudlyCaps`, `$camelCase` или `$under_score` для именования свойств класса.

Независимо от того, какое соглашение об именах используется, оно ДОЛЖНО применяться последовательно в пределах
обоснованной области видимости. Эта область видимости может быть уровнем поставщика, уровнем пакета, уровнем класса,
или уровнем метода.

### 4.3. Методы

Имена методов ОБЯЗАНЫ бы объявлены в `camelCase()`.
