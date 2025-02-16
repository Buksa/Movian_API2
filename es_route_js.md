# Route Module Functions

Модуль `route` предоставляет функции для работы с маршрутами (routes) в ECMAScript. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`route.create(pattern)`**

- **Описание**: Создает новый маршрут на основе регулярного выражения.
- **Параметры**:
  - `pattern` (`string`): Регулярное выражение для маршрута
- **Возвращаемое значение**: `Object` - Созданный маршрут
- **Пример**:
    ```js
    var myRoute = route.create('^/path/to/resource');
    ```

### 2. **`route.backendOpen(prop, url, sync)`**

- **Описание**: Открывает URL через бэкенд.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `url` (`string`): URL для открытия
  - `sync` (`boolean`): Синхронное выполнение
- **Пример**:
    ```js
    route.backendOpen(myProp, 'https://example.com', false);
    ```

### 3. **`route.test(url)`**

- **Описание**: Проверяет, соответствует ли URL какому-либо маршруту.
- **Параметры**:
  - `url` (`string`): URL для проверки
- **Возвращаемое значение**: `boolean` - Соответствует ли URL маршруту
- **Пример**:
    ```js
    var matches = route.test('https://example.com/path/to/resource');
    console.log('Matches:', matches);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля route

// Создание маршрута
var myRoute = route.create('^/path/to/resource');

// Проверка URL
var matches = route.test('https://example.com/path/to/resource');
console.log('Matches:', matches);

// Открытие URL через бэкенд
route.backendOpen(myProp, 'https://example.com', false);
