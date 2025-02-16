# Документация модуля `io`

Модуль `io` предоставляет функции для выполнения HTTP-запросов, создания инспекторов HTTP-запросов, проверки доступности серверов и выполнения XML-RPC запросов. Ниже приведено подробное описание каждой функции и примеры их использования.

---

## Функции

### 1. `httpReq(url, options, callback)`
Выполняет HTTP-запрос.

- **Аргументы**:
  - `url` (строка): URL-адрес для запроса.
  - `options` (объект): Опции запроса:
    - `debug` (булево): Включить отладку.
    - `noFollow` (булево): Не следовать перенаправлениям.
    - `compression` (булево): Включить сжатие.
    - `noAuth` (булево): Отключить авторизацию.
    - `noFail` (булево): Не завершать запрос при ошибке.
    - `verifySSL` (булево): Проверять SSL-сертификат.
    - `headRequest` (булево): Выполнить HEAD-запрос.
    - `cacheTime` (число): Время кэширования в секундах.
    - `caching` (булево): Включить кэширование.
    - `headers` (объект): Заголовки запроса.
    - `postdata` (строка/буфер/объект): Данные для POST-запроса.
    - `method` (строка): Метод запроса (GET, POST и т.д.).
    - `args` (объект): Дополнительные аргументы запроса.
  - `callback` (функция): Функция обратного вызова для асинхронного режима.
- **Возвращает**: В синхронном режиме возвращает объект с результатом запроса. В асинхронном режиме возвращает `undefined`.
- **Пример**:
  ```javascript
  var io = require('native/io');

  // Синхронный запрос
  var result = io.httpReq('https://example.com', {
    method: 'GET',
    headers: {
      'User-Agent': 'MyApp'
    }
  });
  console.log('Результат:', result);

  // Асинхронный запрос
  io.httpReq('https://example.com', {
    method: 'GET'
  }, function(err, res) {
    if (err) {
      console.error('Ошибка:', err);
    } else {
      console.log('Результат:', res);
    }
  });
  ```

---

### 2. `httpInspectorCreate(pattern, callback, async)`
Создает инспектор HTTP-запросов.

- **Аргументы**:
  - `pattern` (строка): Регулярное выражение для фильтрации URL.
  - `callback` (функция): Функция обратного вызова для обработки запроса.
  - `async` (булево): Асинхронный режим работы.
- **Возвращает**: Объект инспектора.
- **Пример**:
  ```javascript
  var io = require('native/io');

  var inspector = io.httpInspectorCreate('^https://example.com', function(req) {
    console.log('Запрос к example.com:', req.url);
    req.proceed(); // Продолжить выполнение запроса
  }, true);
  ```

---

## Функции инспектора HTTP-запросов

Инспектор HTTP-запросов создается с помощью функции `httpInspectorCreate`. После создания инспектора, он может использовать следующие методы для управления запросами:

### 2.1 `fail(reason)`
Отменяет запрос и возвращает ошибку.

- **Аргументы**:
  - `reason` (строка): Причина отмены запроса.
- **Пример**:
  ```javascript
  req.fail("Доступ запрещен");
  ```

---

### 2.2 `proceed()`
Продолжает выполнение запроса без изменений.

- **Пример**:
  ```javascript
  req.proceed();
  ```

---

### 2.3 `ignore()`
Игнорирует запрос, позволяя другим инспекторам обработать его.

- **Пример**:
  ```javascript
  req.ignore();
  ```

---

### 2.4 `setHeader(key, value)`
Добавляет или изменяет заголовок запроса.

- **Аргументы**:
  - `key` (строка): Имя заголовка.
  - `value` (строка): Значение заголовка.
- **Пример**:
  ```javascript
  req.setHeader("X-Custom-Header", "value");
  ```

---

### 2.5 `setCookie(key, value)`
Добавляет или изменяет куку запроса.

- **Аргументы**:
  - `key` (строка): Имя куки.
  - `value` (строка или `null`): Значение куки. Если `null`, кука будет удалена.
- **Пример**:
  ```javascript
  req.setCookie("session_id", "12345");
  req.setCookie("old_cookie", null); // Удаляет куку
  ```

---

## Пример использования инспектора HTTP-запросов полный пример использования всех функций

```javascript
var io = require('native/io');

// Создаем инспектор для всех запросов на example.com
var inspector = io.httpInspectorCreate('^https://example.com', function(req) {
  console.log('Запрос к example.com:', req.url);

  // Добавляем кастомный заголовок
  req.setHeader('X-Custom-Header', 'MyValue');

  // Устанавливаем куку
  req.setCookie('session_id', '12345');

  // Проверяем, есть ли кука "session_id"
  if (!req.cookies || !req.cookies.session_id) {
    req.fail("Отсутствует session_id");
    return;
  }

  // Продолжаем запрос
  req.proceed();
}, true);

// Пример HTTP-запроса, который будет обработан инспектором
io.httpReq('https://example.com', {
  method: 'GET'
}, function(err, res) {
  if (err) {
    console.error('Ошибка:', err);
  } else {
    console.log('Результат:', res);
  }
});
```

---

## Примечания

- Инспекторы HTTP-запросов позволяют гибко управлять запросами, добавлять заголовки, управлять куками и принимать решения о продолжении или отмене запроса.
- Используйте асинхронный режим для обработки запросов в фоновом режиме.
- Убедитесь, что регулярные выражения для фильтрации URL корректны, чтобы инспектор работал только с нужными запросами.

Этот модуль подходит для задач, таких как обработка запросов, добавление кастомных заголовков, управление куками и контроль доступа.

### 3. `probe(url, timeout)`
Проверяет доступность сервера.

- **Аргументы**:
  - `url` (строка): URL-адрес для проверки.
  - `timeout` (число): Таймаут в миллисекундах.
- **Возвращает**: Объект с результатом проверки:
  - `result` (число): Результат проверки (например, `BACKEND_PROBE_OK`).
  - `errmsg` (строка): Сообщение об ошибке (если есть).
- **Пример**:
  ```javascript
  var io = require('native/io');

  var result = io.probe('https://example.com', 5000);
  console.log('Результат проверки:', result);
  ```

---

### 4. `xmlrpc(url, method, json)`
Выполняет XML-RPC запрос.

- **Аргументы**:
  - `url` (строка): URL-адрес XML-RPC сервера.
  - `method` (строка): Метод XML-RPC.
  - `json` (строка): Аргументы в формате JSON.
- **Возвращает**: Объект с результатом запроса.
- **Пример**:
  ```javascript
  var io = require('native/io');

  var result = io.xmlrpc('https://example.com/xmlrpc', 'example.method', '{"param1": "value1"}');
  console.log('Результат XML-RPC:', result);
  ```

---

## Пример использования

Пример использования модуля `io` в среде JavaScript (ES5.1):

### HTTP-запрос
```javascript
var io = require('native/io');

// Синхронный GET-запрос
var result = io.httpReq('https://example.com', {
  method: 'GET',
  headers: {
    'User-Agent': 'MyApp'
  }
});
console.log('Результат:', result);

// Асинхронный POST-запрос
io.httpReq('https://example.com', {
  method: 'POST',
  postdata: { key: 'value' }
}, function(err, res) {
  if (err) {
    console.error('Ошибка:', err);
  } else {
    console.log('Результат:', res);
  }
});
```

### Инспектор HTTP-запросов
```javascript
var io = require('native/io');

var inspector = io.httpInspectorCreate('^https://example.com', function(req) {
  console.log('Запрос к example.com:', req.url);
  req.setHeader('X-Custom-Header', 'value');
  req.proceed(); // Продолжить выполнение запроса
}, true);
```

### Проверка доступности сервера
```javascript
var io = require('native/io');

var result = io.probe('https://example.com', 5000);
console.log('Результат проверки:', result);
```

### XML-RPC запрос
```javascript
var io = require('native/io');

var result = io.xmlrpc('https://example.com/xmlrpc', 'example.method', '{"param1": "value1"}');
console.log('Результат XML-RPC:', result);
```

---

## Примечания

- Модуль `io` предоставляет мощные инструменты для работы с HTTP-запросами, инспекции запросов и выполнения XML-RPC запросов.
- Для асинхронных операций используйте функцию обратного вызова.
- Убедитесь, что URL-адреса и параметры корректны, чтобы избежать ошибок.

Этот модуль подходит для задач, таких как взаимодействие с веб-сервисами, мониторинг доступности серверов и интеграция с XML-RPC API.
