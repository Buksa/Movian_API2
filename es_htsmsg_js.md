# HTSMSG Module Functions

Модуль `htsmsg` предоставляет функции для работы с сообщениями HTS. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`htsmsg.createFromXML(xml)`**

- **Описание**: Создает объект сообщения HTS из XML строки.
- **Параметры**:
  - `xml` (`string`): XML строка для преобразования
- **Возвращаемое значение**: `Object` - Объект сообщения HTS
- **Пример**:
    ```js
    var msg = htsmsg.createFromXML('<root><item>value</item></root>');
    console.log('Message:', msg);
    ```

### 2. **`htsmsg.get(msg, key)`**

- **Описание**: Получает значение из сообщения HTS по ключу или индексу.
- **Параметры**:
  - `msg` (`Object`): Объект сообщения HTS
  - `key` (`string`|`number`): Ключ или индекс значения
- **Возвращаемое значение**: `Object` - Объект с полями `msg` и `value`
- **Пример**:
    ```js
    var value = htsmsg.get(msg, 'item');
    console.log('Value:', value);
    ```

### 3. **`htsmsg.enumerate(msg)`**

- **Описание**: Возвращает массив ключей сообщения HTS.
- **Параметры**:
  - `msg` (`Object`): Объект сообщения HTS
- **Возвращаемое значение**: `Array` - Массив ключей
- **Пример**:
    ```js
    var keys = htsmsg.enumerate(msg);
    console.log('Keys:', keys);
    ```

### 4. **`htsmsg.length(msg)`**

- **Описание**: Возвращает количество элементов в сообщении HTS.
- **Параметры**:
  - `msg` (`Object`): Объект сообщения HTS
- **Возвращаемое значение**: `number` - Количество элементов
- **Пример**:
    ```js
    var length = htsmsg.length(msg);
    console.log('Length:', length);
    ```

### 5. **`htsmsg.getName(msg, index)`**

- **Описание**: Получает имя элемента по индексу.
- **Параметры**:
  - `msg` (`Object`): Объект сообщения HTS
  - `index` (`number`): Индекс элемента
- **Возвращаемое значение**: `string` - Имя элемента
- **Пример**:
    ```js
    var name = htsmsg.getName(msg, 0);
    console.log('Name:', name);
    ```

### 6. **`htsmsg.print(msg)`**

- **Описание**: Выводит сообщение HTS в лог.
- **Параметры**:
  - `msg` (`Object`): Объект сообщения HTS
- **Пример**:
    ```js
    htsmsg.print(msg);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля htsmsg
var xml = '<root><item>value</item></root>';

// Создание сообщения из XML
var msg = htsmsg.createFromXML(xml);

// Получение значения по ключу
var value = htsmsg.get(msg, 'item');
console.log('Value:', value);

// Перечисление ключей
var keys = htsmsg.enumerate(msg);
console.log('Keys:', keys);

// Получение длины сообщения
var length = htsmsg.length(msg);
console.log('Length:', length);

// Получение имени элемента по индексу
var name = htsmsg.getName(msg, 0);
console.log('Name:', name);

// Вывод сообщения в лог
htsmsg.print(msg);
