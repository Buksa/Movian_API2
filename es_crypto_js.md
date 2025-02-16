# Crypto Module Functions

Модуль `crypto` предоставляет функции для работы с криптографическими хэшами. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`crypto.hashCreate(algo)`**

- **Описание**: Создает объект хэша для указанного алгоритма.
- **Параметры**:
  - `algo` (`string`): Алгоритм хэширования:
    - `"sha1"`: SHA-1
    - `"sha256"`: SHA-256
    - `"sha512"`: SHA-512
    - `"md5"`: MD5
- **Возвращаемое значение**: `Object` - Объект хэша
- **Пример**:
    ```js
    var hash = crypto.hashCreate('sha256');
    ```

### 2. **`crypto.hashUpdate(hash, data)`**

- **Описание**: Добавляет данные для хэширования.
- **Параметры**:
  - `hash` (`Object`): Объект хэша
  - `data` (`string`|`Buffer`): Данные для хэширования
- **Пример**:
    ```js
    crypto.hashUpdate(hash, 'Hello, world!');
    ```

### 3. **`crypto.hashFinalize(hash)`**

- **Описание**: Завершает хэширование и возвращает результат.
- **Параметры**:
  - `hash` (`Object`): Объект хэша
- **Возвращаемое значение**: `Buffer` - Хэш-значение
- **Пример**:
    ```js
    var result = crypto.hashFinalize(hash);
    console.log('Hash:', result.toString('hex'));
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля crypto

// Создание хэша SHA-256
var hash = crypto.hashCreate('sha256');

// Добавление данных для хэширования
crypto.hashUpdate(hash, 'Hello, world!');

// Получение результата хэширования
var result = crypto.hashFinalize(hash);
console.log('SHA-256 hash:', result.toString('hex'));
