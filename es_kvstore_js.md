# KVStore Module Functions

Модуль `kvstore` предоставляет функции для работы с хранилищем ключ-значение. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`kvstore.getString(url, domain, key)`**

- **Описание**: Получает строковое значение по ключу.
- **Параметры**:
  - `url` (`string`): URL связанный с данными
  - `domain` (`string`): Домен данных (например, "plugin")
  - `key` (`string`): Ключ значения
- **Возвращаемое значение**: `string` - Значение или `undefined`, если ключ не найден
- **Пример**:
    ```js
    var value = kvstore.getString('https://example.com', 'plugin', 'setting');
    if(value !== undefined) {
      console.log('Value:', value);
    }
    ```

### 2. **`kvstore.getInteger(url, domain, key, defaultValue)`**

- **Описание**: Получает целочисленное значение по ключу.
- **Параметры**:
  - `url` (`string`): URL связанный с данными
  - `domain` (`string`): Домен данных
  - `key` (`string`): Ключ значения
  - `defaultValue` (`number`): Значение по умолчанию, если ключ не найден
- **Возвращаемое значение**: `number` - Значение или значение по умолчанию
- **Пример**:
    ```js
    var count = kvstore.getInteger('https://example.com', 'plugin', 'count', 0);
    console.log('Count:', count);
    ```

### 3. **`kvstore.getBoolean(url, domain, key, defaultValue)`**

- **Описание**: Получает булево значение по ключу.
- **Параметры**:
  - `url` (`string`): URL связанный с данными
  - `domain` (`string`): Домен данных
  - `key` (`string`): Ключ значения
  - `defaultValue` (`boolean`): Значение по умолчанию, если ключ не найден
- **Возвращаемое значение**: `boolean` - Значение или значение по умолчанию
- **Пример**:
    ```js
    var enabled = kvstore.getBoolean('https://example.com', 'plugin', 'enabled', false);
    if(enabled) {
      console.log('Feature is enabled');
    }
    ```

### 4. **`kvstore.set(url, domain, key, value)`**

- **Описание**: Устанавливает значение по ключу.
- **Параметры**:
  - `url` (`string`): URL связанный с данными
  - `domain` (`string`): Домен данных
  - `key` (`string`): Ключ значения
  - `value` (`string`|`number`|`boolean`): Значение для установки
- **Пример**:
    ```js
    // Установка строкового значения
    kvstore.set('https://example.com', 'plugin', 'name', 'MyPlugin');
    
    // Установка числового значения
    kvstore.set('https://example.com', 'plugin', 'count', 42);
    
    // Установка булевого значения
    kvstore.set('https://example.com', 'plugin', 'enabled', true);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля kvstore
var url = 'https://example.com';
var domain = 'plugin';

// Получение строкового значения
var name = kvstore.getString(url, domain, 'name');
if(name !== undefined) {
  console.log('Name:', name);
}

// Получение целочисленного значения
var count = kvstore.getInteger(url, domain, 'count', 0);
console.log('Count:', count);

// Получение булевого значения
var enabled = kvstore.getBoolean(url, domain, 'enabled', false);
if(enabled) {
  console.log('Feature is enabled');
}

// Установка значений
kvstore.set(url, domain, 'name', 'NewName');
kvstore.set(url, domain, 'count', 100);
kvstore.set(url, domain, 'enabled', true);
