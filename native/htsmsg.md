# Документация модуля `htsmsg`

Модуль `htsmsg` предоставляет функции для работы с сообщениями в формате HTSMSG, которые используются для сериализации и десериализации данных. Этот модуль позволяет создавать сообщения из XML, получать значения полей, перечислять поля и выполнять другие операции с сообщениями. Ниже приведено подробное описание каждой функции и примеры их использования.

---

## Функции

### 1. `createFromXML(xml)`
Создает объект сообщения HTSMSG из XML-строки.

- **Аргументы**:
  - `xml` (строка): XML-строка для десериализации.
- **Возвращает**: Объект сообщения HTSMSG.
- **Пример**:
  ```javascript
  var xml = "<root><item>value</item></root>";
  var msg = htsmsg.createFromXML(xml);
  ```

---

### 2. `get(msg, key)`
Возвращает значение поля из сообщения HTSMSG.

- **Аргументы**:
  - `msg` (объект): Объект сообщения HTSMSG.
  - `key` (строка или число): Имя поля или индекс.
- **Возвращает**: Объект с двумя свойствами:
  - `value`: Значение поля.
  - `msg`: Вложенное сообщение (если поле содержит вложенные данные).
- **Пример**:
  ```javascript
  var value = htsmsg.get(msg, "item");
  console.log("Значение поля:", value.value);
  ```

---

### 3. `enumerate(msg)`
Возвращает массив имен всех полей в сообщении.

- **Аргументы**:
  - `msg` (объект): Объект сообщения HTSMSG.
- **Возвращает**: Массив строк с именами полей.
- **Пример**:
  ```javascript
  var fields = htsmsg.enumerate(msg);
  console.log("Поля сообщения:", fields);
  ```

---

### 4. `length(msg)`
Возвращает количество полей в сообщении.

- **Аргументы**:
  - `msg` (объект): Объект сообщения HTSMSG.
- **Возвращает**: Число полей.
- **Пример**:
  ```javascript
  var count = htsmsg.length(msg);
  console.log("Количество полей:", count);
  ```

---

### 5. `getName(msg, index)`
Возвращает имя поля по индексу.

- **Аргументы**:
  - `msg` (объект): Объект сообщения HTSMSG.
  - `index` (число): Индекс поля.
- **Возвращает**: Имя поля или `undefined`, если поле не найдено.
- **Пример**:
  ```javascript
  var name = htsmsg.getName(msg, 0);
  console.log("Имя первого поля:", name);
  ```

---

### 6. `print(msg)`
Выводит содержимое сообщения в лог.

- **Аргументы**:
  - `msg` (объект): Объект сообщения HTSMSG.
- **Пример**:
  ```javascript
  htsmsg.print(msg);
  ```

---

## Пример использования

Пример использования модуля `htsmsg` в среде JavaScript (ES5.1):

### Создание сообщения из XML
```javascript
var htsmsg = require('native/htsmsg');

var xml = "<root><item>value</item><nested><child>42</child></nested></root>";
var msg = htsmsg.createFromXML(xml);

// Получение значения поля
var item = htsmsg.get(msg, "item");
console.log("Значение поля 'item':", item.value);

// Получение вложенного сообщения
var nested = htsmsg.get(msg, "nested");
console.log("Вложенное сообщение:", nested.msg);

// Перечисление полей
var fields = htsmsg.enumerate(msg);
console.log("Поля сообщения:", fields);

// Получение количества полей
var count = htsmsg.length(msg);
console.log("Количество полей:", count);

// Получение имени поля по индексу
var name = htsmsg.getName(msg, 0);
console.log("Имя первого поля:", name);

// Вывод сообщения в лог
htsmsg.print(msg);
```

---

## Примечания

- Модуль `htsmsg` использует библиотеку HTSMSG для работы с сообщениями, что обеспечивает поддержку сложных структур данных.
- Сообщения могут содержать вложенные данные, что позволяет работать с иерархическими структурами.
- Убедитесь, что XML-строка корректна, чтобы избежать ошибок при десериализации.

Этот модуль предоставляет мощный набор функций для работы с сообщениями, что делает его подходящим для задач, таких как обработка данных, сериализация и десериализация, а также интеграция с внешними системами.
