# Документация модуля `kvstore`

Модуль `kvstore` предоставляет функции для работы с хранилищем ключ-значение (Key-Value Store). Этот модуль позволяет получать и устанавливать значения по ключам, а также управлять различными типами данных (строки, числа, булевы значения). Ниже приведено подробное описание каждой функции и примеры их использования.

---

## Функции

### 1. `getString(url, domain, key)`
Получает строковое значение из хранилища по ключу.

- **Аргументы**:
  - `url` (строка): URL, связанный с данными.
  - `domain` (строка): Домен, к которому относится ключ (например, `"plugin"`).
  - `key` (строка): Ключ для поиска значения.
- **Возвращает**: Строковое значение или `undefined`, если ключ не найден.
- **Пример**:
  ```javascript
  var kvstore = require('native/kvstore');
  var value = kvstore.getString('https://example.com', 'plugin', 'myKey');
  console.log('Значение:', value);
  ```

---

### 2. `getInteger(url, domain, key, defaultValue)`
Получает целочисленное значение из хранилища по ключу.

- **Аргументы**:
  - `url` (строка): URL, связанный с данными.
  - `domain` (строка): Домен, к которому относится ключ (например, `"plugin"`).
  - `key` (строка): Ключ для поиска значения.
  - `defaultValue` (число): Значение по умолчанию, если ключ не найден.
- **Возвращает**: Целочисленное значение или значение по умолчанию.
- **Пример**:
  ```javascript
  var kvstore = require('native/kvstore');
  var value = kvstore.getInteger('https://example.com', 'plugin', 'myKey', 42);
  console.log('Значение:', value);
  ```

---

### 3. `getBoolean(url, domain, key, defaultValue)`
Получает булево значение из хранилища по ключу.

- **Аргументы**:
  - `url` (строка): URL, связанный с данными.
  - `domain` (строка): Домен, к которому относится ключ (например, `"plugin"`).
  - `key` (строка): Ключ для поиска значения.
  - `defaultValue` (булево): Значение по умолчанию, если ключ не найден.
- **Возвращает**: Булево значение или значение по умолчанию.
- **Пример**:
  ```javascript
  var kvstore = require('native/kvstore');
  var value = kvstore.getBoolean('https://example.com', 'plugin', 'myKey', false);
  console.log('Значение:', value);
  ```

---

### 4. `set(url, domain, key, value)`
Устанавливает значение в хранилище по ключу.

- **Аргументы**:
  - `url` (строка): URL, связанный с данными.
  - `domain` (строка): Домен, к которому относится ключ (например, `"plugin"`).
  - `key` (строка): Ключ для установки значения.
  - `value` (строка/число/булево): Значение для установки. Если `undefined`, ключ будет удален.
- **Пример**:
  ```javascript
  var kvstore = require('native/kvstore');

  // Установка строки
  kvstore.set('https://example.com', 'plugin', 'myKey', 'Hello');

  // Установка числа
  kvstore.set('https://example.com', 'plugin', 'myKey', 42);

  // Установка булева значения
  kvstore.set('https://example.com', 'plugin', 'myKey', true);

  // Удаление ключа
  kvstore.set('https://example.com', 'plugin', 'myKey', undefined);
  ```

---

## Пример использования

Пример использования модуля `kvstore` в среде JavaScript (ES5.1):

```javascript
var kvstore = require('native/kvstore');

// Получение строки
var strValue = kvstore.getString('https://example.com', 'plugin', 'myStringKey');
console.log('Строковое значение:', strValue);

// Получение числа
var intValue = kvstore.getInteger('https://example.com', 'plugin', 'myIntKey', 0);
console.log('Целочисленное значение:', intValue);

// Получение булева значения
var boolValue = kvstore.getBoolean('https://example.com', 'plugin', 'myBoolKey', false);
console.log('Булево значение:', boolValue);

// Установка значений
kvstore.set('https://example.com', 'plugin', 'myStringKey', 'New Value');
kvstore.set('https://example.com', 'plugin', 'myIntKey', 123);
kvstore.set('https://example.com', 'plugin', 'myBoolKey', true);

// Удаление ключа
kvstore.set('https://example.com', 'plugin', 'myStringKey', undefined);
```

---

## Примечания

- Модуль `kvstore` предоставляет простой интерфейс для работы с хранилищем ключ-значение.
- Используйте домен `"plugin"` для хранения данных, связанных с плагинами.
- Убедитесь, что URL и ключи корректны, чтобы избежать ошибок при работе с хранилищем.

Этот модуль подходит для задач, таких как хранение настроек, кэширование данных и управление состоянием приложения.
