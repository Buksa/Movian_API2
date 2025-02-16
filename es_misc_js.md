# Misc Module Functions

Модуль `misc` предоставляет вспомогательные функции для работы с кэшем, сетевыми интерфейсами и другими задачами. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`misc.cachePut(stash, key, buffer, maxAge)`**

- **Описание**: Сохраняет данные в кэше.
- **Параметры**:
  - `stash` (`string`): Имя хранилища
  - `key` (`string`): Ключ для сохранения данных
  - `buffer` (`Buffer`): Данные для сохранения
  - `maxAge` (`number`): Время жизни данных в секундах
- **Пример**:
    ```js
    var buffer = new Buffer('Hello, world!');
    misc.cachePut('myStash', 'myKey', buffer, 3600);
    ```

### 2. **`misc.cacheGet(stash, key)`**

- **Описание**: Получает данные из кэша.
- **Параметры**:
  - `stash` (`string`): Имя хранилища
  - `key` (`string`): Ключ для получения данных
- **Возвращаемое значение**: `Buffer` - Данные или `null`, если данные не найдены
- **Пример**:
    ```js
    var data = misc.cacheGet('myStash', 'myKey');
    if(data !== null) {
      console.log('Data:', data.toString());
    }
    ```

### 3. **`misc.systemIpAddress()`**

- **Описание**: Возвращает IP-адрес системы.
- **Возвращаемое значение**: `string` - IP-адрес
- **Пример**:
    ```js
    var ip = misc.systemIpAddress();
    console.log('System IP:', ip);
    ```

## Popup Module Functions

Модуль `popup` предоставляет функции для работы с всплывающими окнами и уведомлениями.

---

### 1. **`popup.webpopup(url, title, trap)`**

- **Описание**: Открывает веб-всплывающее окно.
- **Параметры**:
  - `url` (`string`): URL для открытия
  - `title` (`string`): Заголовок окна
  - `trap` (`string`): URL для перехвата
- **Возвращаемое значение**: `Object` - Результат работы окна:
  - `result` (`string`): Результат (`"trapped"`, `"userclose"`, `"neterror"`, `"error"`)
  - `trappedUrl` (`string`): Перехваченный URL (если есть)
  - `args` (`Object`): Аргументы перехваченного URL
- **Пример**:
    ```js
    var result = popup.webpopup('https://example.com', 'Example', 'https://trap.com');
    console.log('Result:', result.result);
    ```

### 2. **`popup.getAuthCredentials(source, reason, query, id, forceTmp)`**

- **Описание**: Запрашивает учетные данные у пользователя.
- **Параметры**:
  - `source` (`string`): Источник запроса
  - `reason` (`string`): Причина запроса
  - `query` (`boolean`): Запрашивать ли учетные данные, если они не найдены
  - `id` (`string`): Идентификатор запроса
  - `forceTmp` (`boolean`): Использовать временные учетные данные
- **Возвращаемое значение**: `Object` - Учетные данные:
  - `username` (`string`): Имя пользователя
  - `password` (`string`): Пароль
  - `rejected` (`boolean`): Запрос был отклонен
- **Пример**:
    ```js
    var creds = popup.getAuthCredentials('MyApp', 'Login required', true, 'login', false);
    if(!creds.rejected) {
      console.log('Username:', creds.username);
      console.log('Password:', creds.password);
    }
    ```

### 3. **`popup.message(message, ok, cancel)`**

- **Описание**: Отображает всплывающее сообщение.
- **Параметры**:
  - `message` (`string`): Текст сообщения
  - `ok` (`boolean`): Показывать кнопку "OK"
  - `cancel` (`boolean`): Показывать кнопку "Cancel"
- **Возвращаемое значение**: `boolean` - Результат (`true` для "OK", `false` для "Cancel")
- **Пример**:
    ```js
    var result = popup.message('Are you sure?', true, true);
    if(result) {
      console.log('User clicked OK');
    } else {
      console.log('User clicked Cancel');
    }
    ```

### 4. **`popup.textDialog(message, ok, cancel)`**

- **Описание**: Отображает диалог ввода текста.
- **Параметры**:
  - `message` (`string`): Текст сообщения
  - `ok` (`boolean`): Показывать кнопку "OK"
  - `cancel` (`boolean`): Показывать кнопку "Cancel"
- **Возвращаемое значение**: `Object` - Результат:
  - `input` (`string`): Введенный текст
  - `rejected` (`boolean`): Запрос был отклонен
- **Пример**:
    ```js
    var result = popup.textDialog('Enter your name:', true, true);
    if(!result.rejected) {
      console.log('User entered:', result.input);
    }
    ```

### 5. **`popup.notify(text, delay, icon)`**

- **Описание**: Отображает уведомление.
- **Параметры**:
  - `text` (`string`): Текст уведомления
  - `delay` (`number`): Время отображения уведомления в миллисекундах
  - `icon` (`string`): Иконка уведомления
- **Пример**:
    ```js
    popup.notify('Operation completed', 3000, 'success');
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля misc
var buffer = new Buffer('Hello, world!');
misc.cachePut('myStash', 'myKey', buffer, 3600);

var data = misc.cacheGet('myStash', 'myKey');
if(data !== null) {
  console.log('Data:', data.toString());
}

var ip = misc.systemIpAddress();
console.log('System IP:', ip);

// Пример использования модуля popup
var result = popup.webpopup('https://example.com', 'Example', 'https://trap.com');
console.log('Result:', result.result);

var creds = popup.getAuthCredentials('MyApp', 'Login required', true, 'login', false);
if(!creds.rejected) {
  console.log('Username:', creds.username);
  console.log('Password:', creds.password);
}

popup.notify('Operation completed', 3000, 'success');
