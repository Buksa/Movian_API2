# Документация модуля `route`

Модуль `route` предоставляет функции для создания и управления маршрутами (routes) в системе. Маршруты используются для обработки URL-адресов и выполнения соответствующих действий, таких как открытие страниц или вызов функций. Этот модуль полезен для создания гибкой системы маршрутизации в приложениях.

---

## Основные функции

### 1. `create(pattern)`
Создает новый маршрут на основе регулярного выражения.

- **Аргументы**:
  - `pattern` (строка): Регулярное выражение для сопоставления URL.
- **Возвращает**: Объект маршрута.
- **Пример**:
  ```javascript
  var route = require('native/route');
  var myRoute = route.create('^/example/(.*)$');
  ```

---

### 2. `backendOpen(page, url, sync)`
Открывает URL с использованием бэкенда.

- **Аргументы**:
  - `page` (объект): Объект страницы.
  - `url` (строка): URL для открытия.
  - `sync` (булево): Синхронный режим (если `true`, выполнение будет блокирующим).
- **Пример**:
  ```javascript
  var route = require('native/route');
  var page = {}; // Объект страницы
  route.backendOpen(page, 'https://example.com', false);
  ```

---

### 3. `test(url)`
Проверяет, соответствует ли URL какому-либо маршруту.

- **Аргументы**:
  - `url` (строка): URL для проверки.
- **Возвращает**: `true`, если URL соответствует маршруту, иначе `false`.
- **Пример**:
  ```javascript
  var route = require('native/route');
  var isMatch = route.test('/example/path');
  console.log('URL соответствует маршруту:', isMatch);
  ```

---

## Пример использования

### Создание и использование маршрутов

```javascript
var route = require('native/route');

// Создание маршрута для обработки URL вида "/example/(.*)"
var myRoute = route.create('^/example/(.*)$');

// Проверка URL на соответствие маршруту
var isMatch = route.test('/example/path');
console.log('URL соответствует маршруту:', isMatch);

// Открытие URL с использованием бэкенда
var page = {}; // Объект страницы
route.backendOpen(page, 'https://example.com', false);
```

---

### Обработка маршрутов с аргументами

```javascript
var route = require('native/route');

// Создание маршрута для обработки URL вида "/user/([0-9]+)"
var userRoute = route.create('^/user/([0-9]+)$');

// Проверка URL на соответствие маршруту
var isMatch = route.test('/user/123');
console.log('URL соответствует маршруту:', isMatch);

// Открытие URL с использованием бэкенда
var page = {}; // Объект страницы
route.backendOpen(page, 'https://example.com/user/123', false);
```

---

### Использование синхронного режима

```javascript
var route = require('native/route');

// Создание маршрута для обработки URL вида "/sync/(.*)"
var syncRoute = route.create('^/sync/(.*)$');

// Открытие URL в синхронном режиме
var page = {}; // Объект страницы
route.backendOpen(page, 'https://example.com/sync/data', true);
```

---

## Примечания

- Модуль `route` позволяет создавать гибкую систему маршрутизации на основе регулярных выражений.
- Используйте функцию `create` для создания маршрутов и `test` для проверки соответствия URL.
- Функция `backendOpen` позволяет открывать URL с использованием бэкенда, поддерживая как синхронный, так и асинхронный режимы.

Этот модуль подходит для задач, таких как обработка URL, маршрутизация запросов и интеграция с бэкендом.
