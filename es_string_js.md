# String Module Functions

Модуль `string` предоставляет функции для работы со строками, включая кодирование, декодирование, разбор URL и другие операции. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`string.isUtf8(str)`**

- **Описание**: Проверяет, является ли строка корректной UTF-8 строкой.
- **Параметры**:
  - `str` (`string`|`Buffer`): Строка или буфер для проверки
- **Возвращаемое значение**: `boolean` - Является ли строка корректной UTF-8
- **Пример**:
    ```js
    var isUtf8 = string.isUtf8('Hello, world!');
    console.log('Is UTF-8:', isUtf8);
    ```

### 2. **`string.utf8FromBytes(bytes, encoding)`**

- **Описание**: Преобразует байты в строку UTF-8, используя указанную кодировку.
- **Параметры**:
  - `bytes` (`Buffer`): Буфер с байтами
  - `encoding` (`string`): Кодировка (например, `"utf-8"`, `"iso-8859-1"`)
- **Возвращаемое значение**: `string` - Преобразованная строка
- **Пример**:
    ```js
    var str = string.utf8FromBytes(buffer, 'iso-8859-1');
    console.log('String:', str);
    ```

### 3. **`string.entityDecode(str)`**

- **Описание**: Декодирует HTML-сущности в строке.
- **Параметры**:
  - `str` (`string`): Строка с HTML-сущностями
- **Возвращаемое значение**: `string` - Декодированная строка
- **Пример**:
    ```js
    var decoded = string.entityDecode('&amp;<>');
    console.log('Decoded:', decoded); // Вывод: &<>
    ```

### 4. **`string.queryStringSplit(query)`**

- **Описание**: Разбивает строку запроса на объект ключ-значение.
- **Параметры**:
  - `query` (`string`): Строка запроса
- **Возвращаемое значение**: `Object` - Объект с ключами и значениями
- **Пример**:
    ```js
    var query = string.queryStringSplit('name=John&age=30');
    console.log('Name:', query.name); // Вывод: John
    console.log('Age:', query.age);    // Вывод: 30
    ```

### 5. **`string.pathEscape(str)`**

- **Описание**: Экранирует строку для использования в пути URL.
- **Параметры**:
  - `str` (`string`): Строка для экранирования
- **Возвращаемое значение**: `string` - Экранированная строка
- **Пример**:
    ```js
    var escaped = string.pathEscape('path/to/resource');
    console.log('Escaped:', escaped);
    ```

### 6. **`string.paramEscape(str)`**

- **Описание**: Экранирует строку для использования в параметрах URL.
- **Параметры**:
  - `str` (`string`): Строка для экранирования
- **Возвращаемое значение**: `string` - Экранированная строка
- **Пример**:
    ```js
    var escaped = string.paramEscape('param=value');
    console.log('Escaped:', escaped);
    ```

### 7. **`string.durationToString(seconds)`**

- **Описание**: Преобразует количество секунд в строку формата `HH:MM:SS` или `MM:SS`.
- **Параметры**:
  - `seconds` (`number`): Количество секунд
- **Возвращаемое значение**: `string` - Форматированная строка
- **Пример**:
    ```js
    var duration = string.durationToString(3661);
    console.log('Duration:', duration); // Вывод: 1:01:01
    ```

### 8. **`string.parseTime(timeStr)`**

- **Описание**: Преобразует строку времени в количество миллисекунд с начала эпохи Unix.
- **Параметры**:
  - `timeStr` (`string`): Строка времени
- **Возвращаемое значение**: `number` - Количество миллисекунд
- **Пример**:
    ```js
    var time = string.parseTime('2023-01-01T00:00:00Z');
    console.log('Time:', time);
    ```

### 9. **`string.parseURL(url, parseQuery)`**

- **Описание**: Разбирает URL на компоненты.
- **Параметры**:
  - `url` (`string`): URL для разбора
  - `parseQuery` (`boolean`): Разбирать ли строку запроса
- **Возвращаемое значение**: `Object` - Объект с компонентами URL
- **Пример**:
    ```js
    var url = string.parseURL('https://example.com/path?query=value', true);
    console.log('Hostname:', url.hostname); // Вывод: example.com
    console.log('Query:', url.query.query);  // Вывод: value
    ```

### 10. **`string.resolveURL(base, url)`**

- **Описание**: Разрешает относительный URL относительно базового URL.
- **Параметры**:
  - `base` (`string`): Базовый URL
  - `url` (`string`): Относительный URL
- **Возвращаемое значение**: `string` - Полный URL
- **Пример**:
    ```js
    var fullUrl = string.resolveURL('https://example.com', '/path');
    console.log('Full URL:', fullUrl); // Вывод: https://example.com/path
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля string

// Проверка UTF-8
var isUtf8 = string.isUtf8('Hello, world!');
console.log('Is UTF-8:', isUtf8);

// Декодирование HTML-сущностей
var decoded = string.entityDecode('&amp;<>');
console.log('Decoded:', decoded);

// Разбор строки запроса
var query = string.queryStringSplit('name=John&age=30');
console.log('Name:', query.name);
console.log('Age:', query.age);

// Преобразование секунд в строку
var duration = string.durationToString(3661);
console.log('Duration:', duration);

// Разбор URL
var url = string.parseURL('https://example.com/path?query=value', true);
console.log('Hostname:', url.hostname);
console.log('Query:', url.query.query);
