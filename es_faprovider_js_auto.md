# Faprovider Module Functions

Модуль `Faprovider` предоставляет функции для создания и управления пользовательскими провайдерами доступа к файлам. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`Faprovider.register(name, options)`**

- **Описание**: Регистрирует новый провайдер доступа к файлам.
- **Параметры**:
  - `name` (`string`): Имя провайдера
  - `options` (`Object`): Опции провайдера. Свойства:
    - `cacheable` (`boolean`): Разрешает кэширование. По умолчанию: false
    - `redirect` (`boolean`): Поддерживает перенаправления. По умолчанию: false
    - `maxConnections` (`number`): Максимальное количество одновременных соединений. По умолчанию: 10
    - `timeout` (`number`): Таймаут операций в миллисекундах. По умолчанию: 30000
    - `retryCount` (`number`): Количество попыток повторного соединения. По умолчанию: 3

- **Возвращаемое значение**: `Object` - Объект провайдера
- **Пример**:
    ```js
    var provider = Faprovider.register('myprovider', {
      cacheable: true,
      redirect: false
    });
    ```

### 2. **`Faprovider.openRespond(handle, success, result)`**

- **Описание**: Отвечает на запрос открытия файла.
- **Параметры**:
  - `handle` (`Object`): Хэндл файла. Пример входящих данных:
    ```js
    {
      url: 'http://example.com/file.txt',
      flags: 0, // Флаги открытия (например, O_RDONLY)
      errbuf: '', // Буфер для сообщений об ошибках
      errsize: 256 // Размер буфера ошибок
    }
    ```

  - `success` (`boolean`): Успешность операции
  - `result` (`Object`): Результат открытия. Свойства:
    - `size` (`number`): Размер файла в байтах. -1 если неизвестен
    - `type` (`string`): Тип файла. Возможные значения:
      - 'file' - обычный файл
      - 'dir' - директория
      - 'link' - символическая ссылка
    - `mtime` (`number`): Время последней модификации в формате timestamp
    - `permissions` (`string`): Права доступа в формате Unix (например, 'rwxr-xr-x')
    - `metadata` (`Object`): Дополнительные метаданные файла

- **Примеры**:
    ```js
    // Успешное открытие файла
    Faprovider.openRespond(handle, true, {
      size: 1024,
      type: 'file'
    });

    // Ошибка открытия
    Faprovider.openRespond(handle, false, {
      error: 'File not found'
    });
    ```
- **Жизненный цикл handle**:
  1. Создается при вызове open()
  2. Используется для всех операций с файлом
  3. Уничтожается при вызове close()
- **Обработка ошибок**:
  - При ошибке установите success=false
  - Запишите сообщение об ошибке в handle.errbuf


### 3. **`Faprovider.readRespond(handle, size)`**

- **Описание**: Отвечает на запрос чтения данных.
- **Параметры**:
  - `handle` (`Object`): Хэндл файла. Пример входящих данных:
    ```js
    {
      readbuf: Buffer.alloc(1024), // Буфер для чтения данных
      readlen: 1024, // Запрошенное количество байт
      fpos: 0, // Текущая позиция в файле
      url: 'http://example.com/file.txt' // URL файла
    }
    ```

  - `size` (`number`): Количество прочитанных байт:
    - Положительное число: количество прочитанных байт
    - 0: конец файла
    - Отрицательное число: ошибка чтения
- **Примеры**:
    ```js
    // Успешное чтение
    Faprovider.readRespond(handle, 1024);

    // Конец файла
    Faprovider.readRespond(handle, 0);

    // Ошибка чтения
    Faprovider.readRespond(handle, -1);
    ```
- **Особенности**:
  - Данные должны быть записаны в handle.readbuf
  - Позиция handle.fpos обновляется автоматически
  - Для больших файлов используйте потоковое чтение


### 4. **`Faprovider.closeRespond(handle)`**

- **Описание**: Отвечает на запрос закрытия файла.
- **Параметры**:
  - `handle` (`Object`): Хэндл файла. Пример входящих данных:
    ```js
    {
      url: 'http://example.com/file.txt',
      fpos: 1024, // Текущая позиция в файле
      size: 4096 // Размер файла
    }
    ```
    После закрытия:
    - Все операции с handle будут недоступны
    - Ресурсы освобождаются автоматически

- **Примеры**:
    ```js
    // Успешное закрытие
    Faprovider.closeRespond(handle);

    // Закрытие с ошибкой
    handle.errbuf = 'Failed to release resources';
    Faprovider.closeRespond(handle);
    ```
- **Особенности**:
  - Всегда вызывайте closeRespond, даже при ошибках
  - Освобождайте все связанные ресурсы
  - Не используйте handle после закрытия


### 5. **`Faprovider.statRespond(handle, success, size, type, mtime)`**

- **Описание**: Отвечает на запрос получения информации о файле.
- **Параметры**:
  - `handle` (`Object`): Хэндл файла. Пример входящих данных:
    ```js
    {
      url: 'http://example.com/file.txt',
      flags: 0, // Флаги операции
      errbuf: '', // Буфер для сообщений об ошибках
      errsize: 256 // Размер буфера ошибок
    }
    ```

  - `success` (`boolean`): Успешность операции
  - `size` (`number`): Размер файла (-1 если неизвестен)
  - `type` (`string`): Тип файла:
    - 'file': обычный файл
    - 'dir': директория
  - `mtime` (`number`): Время модификации (timestamp)
- **Примеры**:
    ```js
    // Успешное получение информации
    Faprovider.statRespond(handle, true, 1024, 'file', Date.now());

    // Ошибка получения информации
    Faprovider.statRespond(handle, false, -1, '', 0);
    ```
- **Особенности**:
  - Для директорий size может быть -1
  - mtime в миллисекундах с Unix epoch
  - Проверяйте права доступа перед ответом


### 6. **`Faprovider.redirectRespond(handle, success, newUrl)`**

- **Описание**: Отвечает на запрос перенаправления.
- **Параметры**:
  - `handle` (`Object`): Хэндл файла. Пример входящих данных:
    ```js
    {
      url: 'http://example.com/oldfile.txt',
      redirect: '', // Новый URL (если успешно)
      flags: 0 // Флаги операции
    }
    ```

  - `success` (`boolean`): Успешность операции
  - `newUrl` (`string`): Новый URL для перенаправления
- **Примеры**:
    ```js
    // Успешное перенаправление
    Faprovider.redirectRespond(handle, true, 'http://newlocation/file');

    // Ошибка перенаправления
    Faprovider.redirectRespond(handle, false, '');
    ```
- **Особенности**:
  - Проверяйте валидность newUrl
  - Ограничивайте количество редиректов
  - Сохраняйте состояние handle при редиректах


### 7. **`Faprovider.setSize(handle, size)`**

- **Описание**: Устанавливает размер файла.
- **Параметры**:
  - `handle` (`Object`): Хэндл файла. Пример входящих данных:
    ```js
    {
      url: 'http://example.com/file.txt',
      size: 1024, // Текущий размер файла
      fpos: 512 // Текущая позиция в файле
    }
    ```

  - `size` (`number`): Новый размер файла
- **Примеры**:
    ```js
    // Установка размера
    Faprovider.setSize(handle, 1024);

    // Установка неизвестного размера
    Faprovider.setSize(handle, -1);
    ```
- **Особенности**:
  - Используйте -1 для неизвестного размера
  - Размер может изменяться при записи
  - Проверяйте доступное место на диске


## Расширенные примеры использования handle

### Пример 1: Полная реализация файлового провайдера

```js
// Регистрация провайдера
var provider = Faprovider.register('myprovider', {
  cacheable: true,
  redirect: false
});

// Обработка открытия файла
provider.open = function(handle, url) {
  try {
    // Проверка доступа
    if (!checkAccess(url)) {
      Faprovider.openRespond(handle, false, {
        error: 'Access denied'
      });
      return;
    }

    // Получение информации о файле
    var fileInfo = getFileInfo(url);
    
    // Ответ с информацией о файле
    Faprovider.openRespond(handle, true, {
      size: fileInfo.size,
      type: fileInfo.type,
      mtime: fileInfo.mtime
    });
  } catch (err) {
    handle.errbuf = err.message;
    Faprovider.openRespond(handle, false, {
      error: err.message
    });
  }
};


// Обработка чтения данных
provider.read = function(handle, buffer, size, pos) {
  try {
    var bytesRead = readFileData(handle.url, buffer, size, pos);
    Faprovider.readRespond(handle, bytesRead);
  } catch (err) {
    handle.errbuf = err.message;
    Faprovider.readRespond(handle, -1);
  }
};


// Обработка закрытия файла
provider.close = function(handle) {
  try {
    releaseFileResources(handle.url);
    Faprovider.closeRespond(handle);
  } catch (err) {
    handle.errbuf = err.message;
    Faprovider.closeRespond(handle);
  }
};

```

### Пример 2: Асинхронная обработка с использованием Promise

```js
// Асинхронное открытие файла
provider.open = function(handle, url) {
  openFileAsync(url).then(function(fileInfo) {
    Faprovider.openRespond(handle, true, {
      size: fileInfo.size,
      type: fileInfo.type,
      mtime: fileInfo.mtime
    });
  }).catch(function(err) {
    handle.errbuf = err.message;
    Faprovider.openRespond(handle, false, {
      error: err.message
    });
  });
};


// Асинхронное чтение данных
provider.read = function(handle, buffer, size, pos) {
  readFileDataAsync(handle.url, buffer, size, pos)
    .then(function(bytesRead) {
      Faprovider.readRespond(handle, bytesRead);
    })
    .catch(function(err) {
      handle.errbuf = err.message;
      Faprovider.readRespond(handle, -1);
    });
};

```

### Пример 3: Обработка больших файлов с потоковым чтением

```js
// Потоковое чтение данных
provider.read = function(handle, buffer, size, pos) {
  var stream = createReadStream(handle.url, {
    start: pos,
    end: pos + size - 1
  });

  var bytesRead = 0;
  
  stream.on('data', function(chunk) {
    buffer.set(chunk, bytesRead);
    bytesRead += chunk.length;
  });

  stream.on('end', function() {
    Faprovider.readRespond(handle, bytesRead);
  });

  stream.on('error', function(err) {
    handle.errbuf = err.message;
    Faprovider.readRespond(handle, -1);
  });
};

```


## Рекомендации по использованию handle

1. **Управление жизненным циклом**:
   - Всегда освобождайте ресурсы в close()
   - Проверяйте состояние handle перед использованием
   - Используйте try/catch для обработки ошибок

2. **Потоковая обработка**:
   - Для больших файлов используйте потоковое чтение
   - Ограничивайте размер буферов
   - Используйте паузы между чтениями

3. **Асинхронные операции**:
   - Используйте Promise для асинхронных операций
   - Обрабатывайте таймауты
   - Управляйте параллельными запросами

4. **Безопасность**:
   - Проверяйте входные данные
   - Ограничивайте доступ к ресурсам
   - Валидируйте пути и URL

5. **Производительность**:
   - Используйте кэширование метаданных
   - Оптимизируйте операции чтения/записи
   - Минимизируйте использование памяти


1. **Регистрация провайдера**:
   - Указывайте уникальное имя
   - Настройте необходимые опции
   
2. **Обработка операций**:
   - Всегда отвечайте на запросы
   - Обрабатывайте ошибки
   
3. **Производительность**:
   - Используйте асинхронные операции
   - Оптимизируйте чтение данных
   
4. **Безопасность**:
   - Проверяйте входные данные
   - Ограничивайте доступ к ресурсам
   
5. **Кэширование**:
   - Используйте кэширование для статических данных
   - Указывайте время жизни кэша
