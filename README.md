PSR-1: Основной стандарт кода

Этот раздел стандарта содержит то, что следует считать стандартом элементов кода,
которые необходимы для обеспечения высокого уровня технической
совместимости между общим кодом PHP.

Ключевые слова «ОБЯЗАН», «НЕ ОБЯЗАН», «ТРЕБУЕТСЯ», «ДОЛЖЕН», «НЕ ДОЛЖЕН», «СЛЕДУЕТ»,
«НЕ СЛЕДУЕТ», «РЕКОМЕНДУЕТСЯ», «МОЖЕТ» и «ПО ЖЕЛАНИЮ» в этом документе должны быть
интерпретируется, как описано в [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).


1. ОБЗОР

Файлы ОБЯЗАНЫ использовать только теги ```php <?php ``` и ```php <?= ```.

Файлы ОБЯЗАНЫ использовать для кода PHP только UTF-8 без [BOM](https://ru.wikipedia.org/wiki/Маркер_последовательности_байтов).

Файлы ДОЛЖНЫ либо объявлять символы (классы, функции, константы и т.д.) или вызывать побочные эффекты (например, генерировать выходные данные, изменять настройки .ini и т.д.), но НЕ ДОЛЖНЫ делать и то и другое.

Пространства имен и классы ОБЯЗАНЫ следовать «автозагрузке» PSR: [PSR-0, PSR-4].

Названия классов ОБЯЗАНЫ быть объявлены в ```php StudlyCaps ```.

Константы класса ОБЯЗАНЫ быть объявлены в верхнем регистре с разделителями подчеркивания ```php NEW_CONSTANT ```.

Имена методов ОБЯЗАНЫ быть объявлены в ```php camelCase ```.
