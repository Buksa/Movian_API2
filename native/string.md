Этот код предоставляет набор функций для работы со строками в ECMAScript (JavaScript) с использованием движка Duktape. Эти функции включают в себя проверку кодировки UTF-8, преобразование байтов в UTF-8, декодирование HTML-сущностей, разбор URL и многое другое. Давайте разберем каждую функцию и приведем примеры их использования.

---

## Функции модуля `string`

### `isUtf8(input)`
Проверяет, является ли строка или буфер корректной UTF-8 строкой.

**Параметры:**
- `input` (строка или буфер) — Входные данные для проверки.

**Возвращает:**
- `true`, если данные являются корректной UTF-8 строкой.
- `false`, если данные содержат некорректные UTF-8 символы.

**Пример:**
```javascript
var isValid = string.isUtf8("Привет, мир!"); // true
var isValid = string.isUtf8(new Uint8Array([0xC3, 0x28])); // false (некорректный UTF-8)
```

---

### `utf8FromBytes(bytes, encoding)`
Преобразует байты в строку UTF-8 с учетом указанной кодировки.

**Параметры:**
- `bytes` (буфер) — Байты для преобразования.
- `encoding` (строка, опционально) — Кодировка (например, "utf-8", "windows-1251"). Если не указана, выполняется автоопределение.

**Возвращает:**
Строку в кодировке UTF-8.

**Пример:**
```javascript
var bytes = new Uint8Array([0xD0, 0x9F, 0xD1, 0x80, 0xD0, 0xB8, 0xD0, 0xB2, 0xD0, 0xB5, 0xD1, 0x82]);
var str = string.utf8FromBytes(bytes); // "Привет"
var str = string.utf8FromBytes(bytes, "windows-1251"); // Преобразование из Windows-1251
```

---

### `entityDecode(str)`
Декодирует HTML-сущности в строке.

**Параметры:**
- `str` (строка) — Строка с HTML-сущностями.

**Возвращает:**
Строку с декодированными HTML-сущностями.

**Пример:**
```javascript
var decoded = string.entityDecode("Hello &lt;world&gt;!"); // "Hello <world>!"
```

---

### `queryStringSplit(query)`
Разбивает строку запроса (query string) на объект с ключами и значениями.

**Параметры:**
- `query` (строка) — Строка запроса (например, "name=John&age=30").

**Возвращает:**
Объект с ключами и значениями.

**Пример:**
```javascript
var query = string.queryStringSplit("name=John&age=30");
console.log(query.name); // "John"
console.log(query.age);  // "30"
```

---

### `pathEscape(str)`
Экранирует строку для использования в пути URL.

**Параметры:**
- `str` (строка) — Строка для экранирования.

**Возвращает:**
Экранированную строку.

**Пример:**
```javascript
var escaped = string.pathEscape("Hello World!"); // "Hello%20World%21"
```

---

### `paramEscape(str)`
Экранирует строку для использования в параметрах URL.

**Параметры:**
- `str` (строка) — Строка для экранирования.

**Возвращает:**
Экранированную строку.

**Пример:**
```javascript
var escaped = string.paramEscape("Hello World!"); // "Hello+World%21"
```

---

### `durationToString(seconds)`
Преобразует количество секунд в строку формата "HH:MM:SS" или "MM:SS".

**Параметры:**
- `seconds` (число) — Количество секунд.

**Возвращает:**
Строку с временем.

**Пример:**
```javascript
var time = string.durationToString(3661); // "1:01:01"
var time = string.durationToString(125);  // "2:05"
```

---

### `parseTime(timeString)`
Парсит строку времени (например, из HTTP-заголовков) и возвращает количество миллисекунд с эпохи Unix.

**Параметры:**
- `timeString` (строка) — Строка времени (например, "Wed, 21 Oct 2015 07:28:00 GMT").

**Возвращает:**
Количество миллисекунд с 1 января 1970 года.

**Пример:**
```javascript
var ms = string.parseTime("Wed, 21 Oct 2015 07:28:00 GMT"); // 1445412480000
```

---

### `parseURL(url, parseQuery)`
Разбирает URL на компоненты (протокол, хост, путь и т.д.).

**Параметры:**
- `url` (строка) — URL для разбора.
- `parseQuery` (логическое значение) — Если `true`, разбирает строку запроса в объект.

**Возвращает:**
Объект с компонентами URL.

**Пример:**
```javascript
var url = string.parseURL("https://example.com/path?name=John", true);
console.log(url.protocol); // "https:"
console.log(url.hostname); // "example.com"
console.log(url.pathname); // "/path"
console.log(url.query.name); // "John"
```

---

### `resolveURL(base, relative)`
Разрешает относительный URL относительно базового URL.

**Параметры:**
- `base` (строка) — Базовый URL.
- `relative` (строка) — Относительный URL.

**Возвращает:**
Абсолютный URL.

**Пример:**
```javascript
var url = string.resolveURL("https://example.com/path/", "subdir/file.html");
console.log(url); // "https://example.com/path/subdir/file.html"
```

---

## Пример использования модуля

```javascript
// Проверка UTF-8
var isValid = string.isUtf8("Привет, мир!"); // true

// Преобразование байтов в UTF-8
var bytes = new Uint8Array([0xD0, 0x9F, 0xD1, 0x80, 0xD0, 0xB8, 0xD0, 0xB2, 0xD0, 0xB5, 0xD1, 0x82]);
var str = string.utf8FromBytes(bytes); // "Привет"

// Декодирование HTML-сущностей
var decoded = string.entityDecode("Hello &lt;world&gt;!"); // "Hello <world>!"

// Разбор строки запроса
var query = string.queryStringSplit("name=John&age=30");
console.log(query.name); // "John"

// Экранирование пути URL
var escaped = string.pathEscape("Hello World!"); // "Hello%20World%21"

// Преобразование секунд в строку времени
var time = string.durationToString(3661); // "1:01:01"

// Разбор URL
var url = string.parseURL("https://example.com/path?name=John", true);
console.log(url.hostname); // "example.com"

// Разрешение относительного URL
var resolved = string.resolveURL("https://example.com/path/", "subdir/file.html");
console.log(resolved); // "https://example.com/path/subdir/file.html"
```

---

Этот модуль предоставляет мощные инструменты для работы со строками, кодировками, URL и временем в JavaScript, что делает его полезным для обработки данных в веб-приложениях и других сценариях.
