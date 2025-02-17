Вот более подробная документация с примерами для модуля WebSocket, оформленная в стиле документации SQLite:

---

# Документация модуля WebSocket

Этот модуль предоставляет функциональность для работы с WebSocket в ECMAScript (JavaScript) с использованием движка Duktape. Он позволяет создавать WebSocket-клиенты и серверы, а также отправлять и получать сообщения через WebSocket.

---

## Содержание
1. [Функции](#функции)
   - [`clientCreate(url, protocol, onConnect, onInput, onClose)`](#clientcreateurl-protocol-onconnect-oninput-onclose)
   - [`clientSend(ws, data)`](#clientsendws-data)
   - [`serverCreate(path, onOpen, onInput, onClose)`](#servercreatepath-onopen-oninput-onclose)
   - [`send(conn, data)`](#sendconn-data)
   - [`close(conn, code, reason)`](#closeconn-code-reason)
2. [Примеры](#примеры)
   - [WebSocket-клиент](#websocket-клиент)
   - [WebSocket-сервер](#websocket-сервер)
   - [Отправка бинарных данных](#отправка-бинарных-данных)
   - [Закрытие соединения](#закрытие-соединения)

---

## Функции

### `clientCreate(url, protocol, onConnect, onInput, onClose)`
Создает WebSocket-клиент и подключается к указанному URL.

**Параметры:**
- `url` (строка) — URL WebSocket-сервера (например, `ws://example.com` или `wss://example.com`).
- `protocol` (строка, опционально) — Протокол WebSocket.
- `onConnect` (функция) — Функция, вызываемая при успешном подключении.
- `onInput` (функция) — Функция, вызываемая при получении данных.
- `onClose` (функция) — Функция, вызываемая при закрытии соединения.

**Возвращает:**
Объект WebSocket-клиента.

**Пример:**
```javascript
var ws = websocket.clientCreate("ws://example.com", null, function() {
    console.log("Connected!");
}, function(data) {
    console.log("Received:", data);
}, function(code, reason) {
    console.log("Closed:", code, reason);
});
```

---

### `clientSend(ws, data)`
Отправляет данные через WebSocket-клиент.

**Параметры:**
- `ws` (объект) — Объект WebSocket-клиента.
- `data` (строка или буфер) — Данные для отправки.

**Пример:**
```javascript
websocket.clientSend(ws, "Hello, server!");
websocket.clientSend(ws, new Uint8Array([1, 2, 3]).buffer); // Отправка бинарных данных
```

---

### `serverCreate(path, onOpen, onInput, onClose)`
Создает WebSocket-сервер на указанном пути.

**Параметры:**
- `path` (строка) — Путь, на котором будет доступен WebSocket-сервер.
- `onOpen` (функция) — Функция, вызываемая при подключении клиента.
- `onInput` (функция) — Функция, вызываемая при получении данных от клиента.
- `onClose` (функция) — Функция, вызываемая при отключении клиента.

**Возвращает:**
Объект WebSocket-сервера.

**Пример:**
```javascript
var server = websocket.serverCreate("/ws", function(conn) {
    console.log("Client connected!");
    conn.send("Welcome!");
}, function(conn, data) {
    console.log("Received:", data);
}, function(conn) {
    console.log("Client disconnected!");
});
```

---

### `send(conn, data)`
Отправляет данные через WebSocket-соединение (для сервера).

**Параметры:**
- `conn` (объект) — Объект соединения (передается в `onOpen`).
- `data` (строка или буфер) — Данные для отправки.

**Пример:**
```javascript
conn.send("Hello, client!");
conn.send(new Uint8Array([1, 2, 3]).buffer); // Отправка бинарных данных
```

---

### `close(conn, code, reason)`
Закрывает WebSocket-соединение (для сервера).

**Параметры:**
- `conn` (объект) — Объект соединения (передается в `onOpen`).
- `code` (число, опционально) — Код закрытия (по умолчанию 1001).
- `reason` (строка, опционально) — Причина закрытия.

**Пример:**
```javascript
conn.close(1000, "Normal closure");
```

---

## Примеры

### WebSocket-клиент
```javascript
var ws = websocket.clientCreate("ws://example.com", null, function() {
    console.log("Connected!");
    websocket.clientSend(ws, "Hello, server!");
}, function(data) {
    console.log("Received:", data);
}, function(code, reason) {
    console.log("Closed:", code, reason);
});
```

### WebSocket-сервер
```javascript
var server = websocket.serverCreate("/ws", function(conn) {
    console.log("Client connected!");
    conn.send("Welcome!");
}, function(conn, data) {
    console.log("Received:", data);
    conn.send("Echo: " + data);
}, function(conn) {
    console.log("Client disconnected!");
});
```

### Отправка бинарных данных
```javascript
var ws = websocket.clientCreate("ws://example.com", null, function() {
    console.log("Connected!");
    var buffer = new Uint8Array([1, 2, 3]).buffer;
    websocket.clientSend(ws, buffer);
}, function(data) {
    console.log("Received binary data:", new Uint8Array(data));
}, function(code, reason) {
    console.log("Closed:", code, reason);
});
```

### Закрытие соединения
```javascript
var ws = websocket.clientCreate("ws://example.com", null, function() {
    console.log("Connected!");
    websocket.clientSend(ws, "Hello, server!");
}, function(data) {
    console.log("Received:", data);
}, function(code, reason) {
    console.log("Closed:", code, reason);
});

// Закрытие соединения через 5 секунд
setTimeout(function() {
    ws.close(1000, "Normal closure");
}, 5000);
```

---

Этот модуль предоставляет мощные инструменты для работы с WebSocket, что делает его полезным для реализации реального времени, чатов, игр и других приложений, требующих двусторонней связи.
