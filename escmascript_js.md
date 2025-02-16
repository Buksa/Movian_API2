Объект `Core` предоставляет различные утилитные функции для обработки информации о версиях, системных путях, компиляции ресурсов и многое другое. Ниже приведены подробные описания и примеры для каждой функции.

---

## Функции Core

### 1. **`Core.compile(path)`**

- **Описание**: Компилирует JavaScript файл в исполняемую функцию.
- **Параметры**:
  - `path` (`string`): Путь к файлу для компиляции. Может быть:
    - Абсолютным путем на диске
    - Относительным путем от корня проекта
    - URL к удаленному ресурсу
- **Возвращаемое значение**: `Function` - Скомпилированная функция
- **Ошибки**:
  - `Error`: Если файл не найден, синтаксическая ошибка в коде или ошибка доступа к файлу
- **Примеры**:
    ```js
    // Компиляция локального файла
    var fn = Core.compile('scripts/main.js');
    fn();
    
    // Компиляция с обработкой ошибок
    try {
      var fn = Core.compile('invalid/path.js');
      fn();
    } catch (e) {
      console.error('Ошибка компиляции:', e.message);
    }
    
    // Компиляция удаленного скрипта
    var fn = Core.compile('https://example.com/script.js');
    fn();
    ```

### 2. **`Core.resourceDestroy(resource)`**

- **Описание**: Уничтожает указанный ресурс для освобождения памяти.
- **Параметры**:
  - `resource` (`Object`): Ресурс для уничтожения
- **Возвращаемое значение**: `void`
- **Пример**:
    ```js
    Core.resourceDestroy(myResource);
    console.log('Ресурс успешно уничтожен');
    ```

### 3. **`Core.sleep(seconds)`**

- **Описание**: Приостанавливает выполнение на указанное количество секунд.
- **Параметры**:
  - `seconds` (`number`): Количество секунд для ожидания
- **Возвращаемое значение**: `void`
- **Пример**:
    ```js
    console.log('Начало ожидания');
    Core.sleep(2.5); // Ожидание 2.5 секунды
    console.log('Ожидание завершено');
    ```

### 4. **`Core.timestamp()`**

- **Описание**: Возвращает текущую метка времени в миллисекундах.
- **Возвращаемое значение**: `number` - Текущая метка времени
- **Пример**:
    ```js
    var start = Core.timestamp();
    // Выполнение какой-либо операции
    var end = Core.timestamp();
    console.log('Операция заняла:', end - start, 'мс');
    ```

### 5. **`Core.randomBytes(length)`**

- **Описание**: Генерирует случайную последовательность байтов.
- **Параметры**:
  - `length` (`number`): Количество байтов для генерации
- **Возвращаемое значение**: `Uint8Array` - Массив случайных байтов
- **Пример**:
    ```js
    var randomData = Core.randomBytes(32);
    console.log('Сгенерированные случайные данные:', randomData);
    ```

### 6. **`Core.currentVersionInt()`**

- **Описание**: Возвращает текущую версию ядра в виде целого числа.
- **Возвращаемое значение**: `number` - Текущая версия в формате целого числа
- **Пример**:
    ```js
    var version = Core.currentVersionInt();
    console.log(version);  // Пример: 1020 (версия 1.2.0)
    ```

### 7. **`Core.currentVersionString()`**

- **Описание**: Возвращает текущую версию ядра в виде строки.
- **Возвращаемое значение**: `string` - Текущая версия в виде строки
- **Пример**:
    ```js
    var version = Core.currentVersionString();
    console.log(version);  // Пример: '1.2.0'
    ```

### 8. **`Core.deviceId()`**

- **Описание**: Возвращает уникальный идентификатор устройства.
- **Возвращаемое значение**: `string` - Уникальный идентификатор устройства
- **Пример**:
    ```js
    var deviceId = Core.deviceId();
    console.log(deviceId);  // Пример: 'device-1234567890'
    ```

### 9. **`Core.loadPath()`**

- **Описание**: Возвращает путь загрузки ресурсов.
- **Возвращаемое значение**: `string` - Путь для загрузки ресурсов
- **Пример**:
    ```js
    var path = Core.loadPath();
    console.log(path);  // Пример: '/path/to/resources'
    ```

### 10. **`Core.storagePath()`**

- **Описание**: Возвращает путь для хранения данных.
- **Возвращаемое значение**: `string` - Путь для хранения данных
- **Пример**:
    ```js
    var path = Core.storagePath();
    console.log(path);  // Пример: '/path/to/storage'
    ```

## Функции таймеров (Timer)

### `setTimeout(callback, delay)`
```javascript
/**
 * Устанавливает таймер для выполнения функции
 * @param {Function} callback - Функция для выполнения
 * @param {number} delay - Задержка в миллисекундах
 * @returns {number} ID таймера
 */
var timerId = setTimeout(function() {
  console.log('Выполнено через 1 секунду');
}, 1000);
```

### `clearTimeout(timerId)`
```javascript
/**
 * Отменяет таймер
 * @param {number} timerId - ID таймера для отмены
 */
clearTimeout(timerId);
```

### `setInterval(callback, interval)`
```javascript
/**
 * Устанавливает интервал для повторного выполнения функции
 * @param {Function} callback - Функция для выполнения
 * @param {number} interval - Интервал в миллисекундах
 * @returns {number} ID интервала
 */
var intervalId = setInterval(function() {
  console.log('Выполняется каждую секунду');
}, 1000);
```

### `clearInterval(intervalId)`
```javascript
/**
 * Отменяет интервал
 * @param {number} intervalId - ID интервала для отменя
 */
clearInterval(intervalId);
```

## Функции консоли (Console)

### `console.log(...args)`
```javascript
/**
 * Логирует сообщения
 * @param {...any} args - Аргументы для логирования
 */
console.log('Простое сообщение', { key: 'value' });
```

### `console.info(...args)`
```javascript
/**
 * Логирует информационные сообщения
 * @param {...any} args - Аргументы для логирования
 */
console.info('Информационное сообщение');
```

### `console.warn(...args)`
```javascript
/**
 * Логирует предупреждения
 * @param {...any} args - Аргументы для логирования
 */
console.warn('Предупреждение!');
```

### `console.error(...args)`
```javascript
/**
 * Логирует ошибки
 * @param {...any} args - Аргументы для логирования
 */
console.error('Произошла ошибка!');
