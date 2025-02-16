# WebSocket Module Functions

Модуль `websocket` предоставляет функции для работы с WebSocket-клиентами и серверами. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`websocket.clientCreate(url, protocol, callback)`**

- **Описание**: Создает WebSocket-клиент для подключения к указанному URL.
- **Параметры**:
  - `url` (`string`): URL для подключения (например, `"ws://example.com"`)
  - `protocol` (`string`): Протокол WebSocket (опционально)
  - `callback` (`function`): Функция обратного вызова для обработки событий
- **Возвращаемое значение**: `Object` - Объект WebSocket-клиента
- **Пример**:
    ```js
    var ws = websocket.clientCreate('ws://example.com', null, {
      onConnect: function() {
        console.log('Connected');
      },
      onInput: function(data) {
        console.log('Received:', data);
      },
      onClose: function(code, reason) {
        console.log('Closed:', code, reason);
      }
    });
    ```

### 2. **`websocket.clientSend(client, data)`**

- **Описание**: Отправляет данные через WebSocket-клиент.
- **Параметры**:
  - `client` (`Object`): Объект WebSocket-клиента
  - `data` (`string`|`Buffer`): Данные для отправки
- **Пример**:
    ```js
    websocket.clientSend(ws, 'Hello, server!');
    ```

### 3. **`websocket.serverCreate(path, callback)`**

- **Описание**: Создает WebSocket-сервер на указанном пути.
- **Параметры**:
  - `path` (`string`): Путь для сервера (например, `"/ws"`)
  - `callback` (`function`): Функция обратного вызова для обработки событий
- **Возвращаемое значение**: `Object` - Объект WebSocket-сервера
- **Пример**:
    ```js
    var server = websocket.serverCreate('/ws', {
      onOpen: function(connection) {
        console.log('New connection');
      },
      onInput: function(connection, data) {
        console.log('Received:', data);
      },
      onClose: function(connection) {
        console.log('Connection closed');
      }
    });
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля websocket

// Создание WebSocket-клиента
var ws = websocket.clientCreate('ws://example.com', null, {
  onConnect: function() {
    console.log('Connected');
  },
  onInput: function(data) {
    console.log('Received:', data);
  },
  onClose: function(code, reason) {
    console.log('Closed:', code, reason);
  }
});

// Отправка данных через WebSocket-клиент
websocket.clientSend(ws, 'Hello, server!');

// Создание WebSocket-сервера
var server = websocket.serverCreate('/ws', {
  onOpen: function(connection) {
    console.log('New connection');
  },
  onInput: function(connection, data) {
    console.log('Received:', data);
  },
  onClose: function(connection) {
    console.log('Connection closed');
  }
});
