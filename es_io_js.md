# IO Module Functions

Модуль `io` предоставляет функции для работы с вводом-выводом. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`io.httpReq(url, options, callback)`**

- **Описание**: Выполняет HTTP запрос.
- **Параметры**:
  - `url` (`string`): URL для запроса
  - `options` (`Object`): Опции запроса:
    - `debug` (`boolean`): Включить отладку
    - `noFollow` (`boolean`): Не следовать перенаправлениям
    - `compression` (`boolean`): Использовать сжатие
    - `noAuth` (`boolean`): Отключить авторизацию
    - `noFail` (`boolean`): Не завершать при ошибке
    - `verifySSL` (`boolean`): Проверять SSL сертификат
    - `headRequest` (`boolean`): Выполнить HEAD запрос
    - `cacheTime` (`number`): Время кэширования в секундах
    - `caching` (`boolean`): Использовать кэширование
    - `headers` (`Object`): Заголовки запроса
    - `postdata` (`string`|`Object`|`Buffer`): Данные для POST запроса
    - `args` (`Object`): Аргументы запроса
    - `method` (`string`): Метод запроса (GET, POST и т.д.)
  - `callback` (`function`): Функция обратного вызова
- **Возвращаемое значение**: `Object` - Объект запроса
- **Пример**:
    ```js
    io.httpReq('https://example.com', {
      method: 'GET',
      headers: {
        'User-Agent': 'MyApp'
      }
    }, function(err, result) {
      if(err) {
        console.error('Error:', err);
        return;
      }
      console.log('Response:', result);
    });
    ```

### 2. **`io.httpInspectorCreate(pattern, callback, async)`**

- **Описание**: Создает инспектор HTTP запросов.
- **Параметры**:
  - `pattern` (`string`): Регулярное выражение для фильтрации URL
  - `callback` (`function`): Функция обратного вызова
  - `async` (`boolean`): Асинхронный режим
- **Возвращаемое значение**: `Object` - Объект инспектора
- **Пример**:
    ```js
    io.httpInspectorCreate('^https://example.com', function(req) {
      console.log('Inspecting request to:', req.url);
      req.proceed();
    }, true);
    ```

### 3. **`io.probe(url, timeout)`**

- **Описание**: Проверяет доступность ресурса.
- **Параметры**:
  - `url` (`string`): URL для проверки
  - `timeout` (`number`): Таймаут в миллисекундах
- **Возвращаемое значение**: `Object` - Результат проверки:
  - `result` (`number`): Код результата
  - `errmsg` (`string`): Сообщение об ошибке
- **Пример**:
    ```js
    var res = io.probe('https://example.com', 5000);
    if(res.result === 0) {
      console.log('Resource is available');
    } else {
      console.error('Error:', res.errmsg);
    }
    ```

### 4. **`io.xmlrpc(url, method, args)`**

- **Описание**: Выполняет XML-RPC запрос.
- **Параметры**:
  - `url` (`string`): URL сервера
  - `method` (`string`): Метод для вызова
  - `args` (`string`): Аргументы в формате JSON
- **Возвращаемое значение**: `Object` - Результат запроса
- **Пример**:
    ```js
    var result = io.xmlrpc('https://example.com/xmlrpc', 'test.method', '{"param": "value"}');
    console.log('Result:', result);
    ```

## Методы объекта HTTP Inspector

### 1. **`req.fail(reason)`**

- **Описание**: Завершает запрос с ошибкой.
- **Параметры**:
  - `reason` (`string`): Причина ошибки
- **Пример**:
    ```js
    req.fail('Invalid request');
    ```

### 2. **`req.proceed()`**

- **Описание**: Продолжает выполнение запроса.
- **Пример**:
    ```js
    req.proceed();
    ```

### 3. **`req.ignore()`**

- **Описание**: Игнорирует запрос.
- **Пример**:
    ```js
    req.ignore();
    ```

### 4. **`req.setHeader(key, value)`**

- **Описание**: Устанавливает заголовок запроса.
- **Параметры**:
  - `key` (`string`): Имя заголовка
  - `value` (`string`): Значение заголовка
- **Пример**:
    ```js
    req.setHeader('User-Agent', 'MyApp');
    ```

### 5. **`req.setCookie(key, value)`**

- **Описание**: Устанавливает cookie для запроса.
- **Параметры**:
  - `key` (`string`): Имя cookie
  - `value` (`string`): Значение cookie
- **Пример**:
    ```js
    req.setCookie('session', '12345');
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля io
io.httpReq('https://api.example.com/data', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer token123'
  }
}, function(err, result) {
  if(err) {
    console.error('Ошибка запроса:', err);
    return;
  }
  
  // Обработка успешного ответа
  console.log('Полученные данные:', result.buffer.toString());
  
  // Создание инспектора для мониторинга запросов
  io.httpInspectorCreate('^https://api.example.com', function(req) {
    console.log('Обнаружен запрос к:', req.url);
    
    // Добавление кастомного заголовка
    req.setHeader('X-Custom-Header', 'value');
    
    // Продолжение выполнения запроса
    req.proceed();
  }, true);
  
  // Проверка доступности ресурса
  var probeResult = io.probe('https://api.example.com', 3000);
  if(probeResult.result === 0) {
    console.log('API доступен');
  } else {
    console.error('API недоступен:', probeResult.errmsg);
  }
  
  // Выполнение XML-RPC запроса
  var xmlrpcResult = io.xmlrpc('https://api.example.com/rpc', 'getData', 
    '{"param1": "value1", "param2": "value2"}');
  console.log('Результат XML-RPC:', xmlrpcResult);
});
