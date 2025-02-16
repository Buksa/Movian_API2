# Документация модулей `misc` и `popup`

Модули `misc` и `popup` предоставляют функции для работы с кэшированием, сетевыми интерфейсами, всплывающими окнами, диалогами и уведомлениями. Эти модули полезны для выполнения различных задач, таких как кэширование данных, получение IP-адреса системы, отображение всплывающих окон и диалогов, а также управление уведомлениями.

---

## Модуль `misc`

### 1. `cachePut(stash, key, buffer, maxage)`
Сохраняет данные в кэше.

- **Аргументы**:
  - `stash` (строка): Имя хранилища кэша.
  - `key` (строка): Ключ для сохранения данных.
  - `buffer` (буфер): Данные для сохранения.
  - `maxage` (число): Время жизни данных в кэше (в секундах).
- **Пример**:
  ```javascript
  var misc = require('misc');
  var buffer = new ArrayBuffer(10);
  misc.cachePut('myStash', 'myKey', buffer, 3600);
  ```

---

### 2. `cacheGet(stash, key)`
Получает данные из кэша.

- **Аргументы**:
  - `stash` (строка): Имя хранилища кэша.
  - `key` (строка): Ключ для получения данных.
- **Возвращает**: Буфер с данными или `null`, если данные не найдены.
- **Пример**:
  ```javascript
  var misc = require('misc');
  var data = misc.cacheGet('myStash', 'myKey');
  if (data) {
    console.log('Данные из кэша:', data);
  } else {
    console.log('Данные не найдены.');
  }
  ```

---

### 3. `systemIpAddress()`
Возвращает IP-адрес системы.

- **Возвращает**: Строку с IP-адресом системы.
- **Пример**:
  ```javascript
  var misc = require('misc');
  var ip = misc.systemIpAddress();
  console.log('IP-адрес системы:', ip);
  ```

---

### 4. `selectView(filename)`
Выбирает представление для указанного файла (если включена поддержка плагинов).

- **Аргументы**:
  - `filename` (строка): Имя файла.
- **Пример**:
  ```javascript
  var misc = require('misc');
  misc.selectView('example.mp4');
  ```

---

## Модуль `popup`

### 1. `webpopup(url, title, trap)`
Открывает всплывающее окно с веб-содержимым.

- **Аргументы**:
  - `url` (строка): URL для загрузки в окне.
  - `title` (строка): Заголовок окна.
  - `trap` (строка): URL, который будет перехвачен при навигации.
- **Возвращает**: Объект с результатом:
  - `result` (строка): Результат (`"trapped"`, `"userclose"`, `"neterror"`, `"error"`).
  - `trappedUrl` (строка): Перехваченный URL (если есть).
  - `args` (объект): Аргументы, переданные с перехваченным URL.
- **Пример**:
  ```javascript
  var popup = require('popup');
  var result = popup.webpopup('https://example.com', 'Example', 'https://example.com/trap');
  console.log('Результат:', result.result);
  if (result.trappedUrl) {
    console.log('Перехваченный URL:', result.trappedUrl);
  }
  ```

---

### 2. `getAuthCredentials(source, reason, query, id, forcetmp)`
Запрашивает учетные данные у пользователя.

- **Аргументы**:
  - `source` (строка): Источник запроса.
  - `reason` (строка): Причина запроса.
  - `query` (булево): Запрашивать ли имя пользователя.
  - `id` (строка): Идентификатор запроса (опционально).
  - `forcetmp` (булево): Принудительно использовать временные учетные данные.
- **Возвращает**: Объект с учетными данными или флагом отклонения:
  - `rejected` (булево): `true`, если запрос отклонен.
  - `username` (строка): Имя пользователя.
  - `password` (строка): Пароль.
- **Пример**:
  ```javascript
  var popup = require('popup');
  var credentials = popup.getAuthCredentials('example.com', 'Login required', true, '123', false);
  if (credentials.rejected) {
    console.log('Запрос отклонен.');
  } else {
    console.log('Имя пользователя:', credentials.username);
    console.log('Пароль:', credentials.password);
  }
  ```

---

### 3. `message(message, ok, cancel)`
Отображает всплывающее окно с сообщением.

- **Аргументы**:
  - `message` (строка): Текст сообщения.
  - `ok` (булево): Показывать ли кнопку "OK".
  - `cancel` (булево): Показывать ли кнопку "Cancel".
- **Возвращает**: `true`, если нажата кнопка "OK", `false` — если "Cancel".
- **Пример**:
  ```javascript
  var popup = require('popup');
  var result = popup.message('Вы уверены?', true, true);
  if (result) {
    console.log('Пользователь нажал OK.');
  } else {
    console.log('Пользователь нажал Cancel.');
  }
  ```

---

### 4. `textDialog(message, ok, cancel)`
Отображает диалог с текстовым вводом.

- **Аргументы**:
  - `message` (строка): Текст сообщения.
  - `ok` (булево): Показывать ли кнопку "OK".
  - `cancel` (булево): Показывать ли кнопку "Cancel".
- **Возвращает**: Объект с результатом:
  - `rejected` (булево): `true`, если запрос отклонен.
  - `input` (строка): Введенный текст.
- **Пример**:
  ```javascript
  var popup = require('popup');
  var result = popup.textDialog('Введите текст:', true, true);
  if (result.rejected) {
    console.log('Запрос отклонен.');
  } else {
    console.log('Введенный текст:', result.input);
  }
  ```

---

### 5. `notify(text, delay, icon)`
Отображает уведомление.

- **Аргументы**:
  - `text` (строка): Текст уведомления.
  - `delay` (число): Время отображения уведомления (в миллисекундах).
  - `icon` (строка): Иконка уведомления (опционально).
- **Пример**:
  ```javascript
  var popup = require('popup');
  popup.notify('Уведомление!', 3000, 'info');
  ```

---

## Пример использования

Пример использования модулей `misc` и `popup` в среде JavaScript (ES5.1):

### Использование кэша
```javascript
var misc = require('misc');

// Сохранение данных в кэше
var buffer = new ArrayBuffer(10);
misc.cachePut('myStash', 'myKey', buffer, 3600);

// Получение данных из кэша
var data = misc.cacheGet('myStash', 'myKey');
if (data) {
  console.log('Данные из кэша:', data);
} else {
  console.log('Данные не найдены.');
}
```

### Получение IP-адреса системы
```javascript
var misc = require('misc');
var ip = misc.systemIpAddress();
console.log('IP-адрес системы:', ip);
```

### Отображение всплывающего окна
```javascript
var popup = require('popup');
var result = popup.webpopup('https://example.com', 'Example', 'https://example.com/trap');
console.log('Результат:', result.result);
if (result.trappedUrl) {
  console.log('Перехваченный URL:', result.trappedUrl);
}
```

### Отображение уведомления
```javascript
var popup = require('popup');
popup.notify('Уведомление!', 3000, 'info');
```

---

## Примечания

- Модуль `misc` предоставляет функции для работы с кэшем, сетевыми интерфейсами и выбора представлений.
- Модуль `popup` позволяет отображать всплывающие окна, диалоги и уведомления, а также запрашивать учетные данные у пользователя.
- Убедитесь, что URL и ключи корректны, чтобы избежать ошибок при работе с кэшем и всплывающими окнами.

Эти модули подходят для задач, таких как кэширование данных, управление сетевыми интерфейсами, отображение пользовательских интерфейсов и уведомлений.
