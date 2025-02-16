# FS Module Functions

Модуль `fs` предоставляет функции для работы с файловой системой. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`fs.open(path, flags)`**

- **Описание**: Открывает файл для чтения или записи.
- **Параметры**:
  - `path` (`string`): Путь к файлу
  - `flags` (`string`): Флаги открытия:
    - `"r"`: Чтение
    - `"w"`: Запись
    - `"a"`: Добавление
- **Возвращаемое значение**: `Object` - Дескриптор файла
- **Пример**:
    ```js
    var fd = fs.open('/path/to/file', 'r');
    ```

### 2. **`fs.read(fd, buffer, offset, length, position)`**

- **Описание**: Читает данные из файла в буфер.
- **Параметры**:
  - `fd` (`Object`): Дескриптор файла
  - `buffer` (`Buffer`): Буфер для записи данных
  - `offset` (`number`): Смещение в буфере
  - `length` (`number`): Количество байт для чтения
  - `position` (`number`): Позиция в файле
- **Возвращаемое значение**: `number` - Количество прочитанных байт
- **Пример**:
    ```js
    var buffer = new Buffer(1024);
    var bytesRead = fs.read(fd, buffer, 0, 1024, 0);
    ```

### 3. **`fs.write(fd, buffer, offset, length, position)`**

- **Описание**: Записывает данные из буфера в файл.
- **Параметры**:
  - `fd` (`Object`): Дескриптор файла
  - `buffer` (`Buffer`): Буфер с данными
  - `offset` (`number`): Смещение в буфере
  - `length` (`number`): Количество байт для записи
  - `position` (`number`): Позиция в файле
- **Возвращаемое значение**: `number` - Количество записанных байт
- **Пример**:
    ```js
    var buffer = new Buffer('Hello');
    var bytesWritten = fs.write(fd, buffer, 0, 5, 0);
    ```

### 4. **`fs.fsize(fd)`**

- **Описание**: Возвращает размер файла.
- **Параметры**:
  - `fd` (`Object`): Дескриптор файла
- **Возвращаемое значение**: `number` - Размер файла в байтах
- **Пример**:
    ```js
    var size = fs.fsize(fd);
    console.log('File size:', size);
    ```

### 5. **`fs.ftruncate(fd, size)`**

- **Описание**: Изменяет размер файла.
- **Параметры**:
  - `fd` (`Object`): Дескриптор файла
  - `size` (`number`): Новый размер файла
- **Пример**:
    ```js
    fs.ftruncate(fd, 1024);
    ```

### 6. **`fs.rename(oldPath, newPath)`**

- **Описание**: Переименовывает файл или директорию.
- **Параметры**:
  - `oldPath` (`string`): Старый путь
  - `newPath` (`string`): Новый путь
- **Пример**:
    ```js
    fs.rename('/old/path', '/new/path');
    ```

### 7. **`fs.mkdirs(path)`**

- **Описание**: Создает директории, включая все необходимые родительские директории.
- **Параметры**:
  - `path` (`string`): Путь к директории
- **Пример**:
    ```js
    fs.mkdirs('/path/to/new/directory');
    ```

### 8. **`fs.dirname(path)`**

- **Описание**: Возвращает директорию из пути.
- **Параметры**:
  - `path` (`string`): Путь к файлу или директории
- **Возвращаемое значение**: `string` - Директория
- **Пример**:
    ```js
    var dir = fs.dirname('/path/to/file');
    console.log('Directory:', dir);
    ```

### 9. **`fs.basename(path)`**

- **Описание**: Возвращает имя файла из пути.
- **Параметры**:
  - `path` (`string`): Путь к файлу
- **Возвращаемое значение**: `string` - Имя файла
- **Пример**:
    ```js
    var name = fs.basename('/path/to/file');
    console.log('File name:', name);
    ```

### 10. **`fs.copyfile(src, dst)`**

- **Описание**: Копирует файл из одного места в другое.
- **Параметры**:
  - `src` (`string`): Путь к исходному файлу
  - `dst` (`string`): Путь к целевому файлу
- **Пример**:
    ```js
    fs.copyfile('/src/file', '/dst/file');
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля fs

// Открытие файла для чтения
var fd = fs.open('/path/to/file', 'r');

// Чтение данных из файла
var buffer = new Buffer(1024);
var bytesRead = fs.read(fd, buffer, 0, 1024, 0);
console.log('Read', bytesRead, 'bytes');

// Получение размера файла
var size = fs.fsize(fd);
console.log('File size:', size);

// Закрытие файла
fs.close(fd);

// Создание директории
fs.mkdirs('/path/to/new/directory');

// Копирование файла
fs.copyfile('/src/file', '/dst/file');
