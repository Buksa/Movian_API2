# Документация модуля `sqlite`

Модуль `sqlite` предоставляет функции для работы с базами данных SQLite. Этот модуль позволяет создавать базы данных, выполнять SQL-запросы, управлять транзакциями и получать информацию о результатах выполнения запросов.

---

## Основные функции

### 1. `create(name)`
Создает новую базу данных SQLite или открывает существующую.

- **Аргументы**:
  - `name` (строка): Имя базы данных.
- **Возвращает**: Объект базы данных.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');
  ```

---

### 2. `query(query, ...args)`
Выполняет SQL-запрос с параметрами.

- **Аргументы**:
  - `query` (строка): SQL-запрос.
  - `args` (опционально): Параметры для запроса.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  // Создание таблицы
  db.query('CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)');

  // Вставка данных
  db.query('INSERT INTO users (name) VALUES (?)', 'John Doe');

  // Выборка данных
  db.query('SELECT * FROM users');
  ```

---

### 3. `step()`
Выполняет шаг выполнения запроса и возвращает текущую строку результата.

- **Возвращает**: Объект с данными текущей строки или `null`, если строк больше нет.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  db.query('SELECT * FROM users');
  while (true) {
    var row = db.step();
    if (row === null) break;
    console.log('User:', row.name);
  }
  ```

---

### 4. `changes()`
Возвращает количество строк, измененных последним запросом.

- **Возвращает**: Число измененных строк.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  db.query('UPDATE users SET name = ? WHERE id = ?', 'Jane Doe', 1);
  var changes = db.changes();
  console.log('Изменено строк:', changes);
  ```

---

### 5. `lastErrorCode()`
Возвращает код последней ошибки.

- **Возвращает**: Код ошибки.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  try {
    db.query('INVALID SQL QUERY');
  } catch (e) {
    console.log('Код ошибки:', db.lastErrorCode());
  }
  ```

---

### 6. `lastErrorString()`
Возвращает текстовое описание последней ошибки.

- **Возвращает**: Текст ошибки.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  try {
    db.query('INVALID SQL QUERY');
  } catch (e) {
    console.log('Ошибка:', db.lastErrorString());
  }
  ```

---

### 7. `lastRowId()`
Возвращает идентификатор последней вставленной строки.

- **Возвращает**: Идентификатор строки.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  db.query('INSERT INTO users (name) VALUES (?)', 'John Doe');
  var lastId = db.lastRowId();
  console.log('ID последней вставленной строки:', lastId);
  ```

---

### 8. `upgradeSchema(schema)`
Обновляет схему базы данных до указанной версии.

- **Аргументы**:
  - `schema` (строка): SQL-скрипт для обновления схемы.
- **Пример**:
  ```javascript
  var sqlite = require('sqlite');
  var db = sqlite.create('myDatabase');

  var schema = `
    CREATE TABLE IF NOT EXISTS users (
      id INTEGER PRIMARY KEY,
      name TEXT
    );
  `;
  db.upgradeSchema(schema);
  ```

---

## Пример использования

### Создание базы данных и выполнение запросов

```javascript
var sqlite = require('sqlite');

// Создание базы данных
var db = sqlite.create('myDatabase');

// Создание таблицы
db.query('CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)');

// Вставка данных
db.query('INSERT INTO users (name) VALUES (?)', 'John Doe');
db.query('INSERT INTO users (name) VALUES (?)', 'Jane Doe');

// Выборка данных
db.query('SELECT * FROM users');
while (true) {
  var row = db.step();
  if (row === null) break;
  console.log('User:', row.id, row.name);
}

// Обновление данных
db.query('UPDATE users SET name = ? WHERE id = ?', 'John Smith', 1);
console.log('Изменено строк:', db.changes());

// Получение ID последней вставленной строки
var lastId = db.lastRowId();
console.log('ID последней вставленной строки:', lastId);
```

---

### Обработка ошибок

```javascript
var sqlite = require('sqlite');
var db = sqlite.create('myDatabase');

try {
  // Попытка выполнить неверный запрос
  db.query('INVALID SQL QUERY');
} catch (e) {
  console.log('Произошла ошибка:');
  console.log('Код ошибки:', db.lastErrorCode());
  console.log('Текст ошибки:', db.lastErrorString());
}
```

---

### Обновление схемы базы данных

```javascript
var sqlite = require('sqlite');
var db = sqlite.create('myDatabase');

// Определение схемы
var schema = `
  CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY,
    name TEXT,
    email TEXT
  );
`;

// Обновление схемы
db.upgradeSchema(schema);

// Проверка обновленной схемы
db.query('SELECT * FROM users');
while (true) {
  var row = db.step();
  if (row === null) break;
  console.log('User:', row.id, row.name, row.email);
}
```

---

## Примечания

- Модуль `sqlite` предоставляет простой интерфейс для работы с базами данных SQLite.
- Используйте функции `query` и `step` для выполнения запросов и обработки результатов.
- Функции `changes`, `lastErrorCode`, `lastErrorString` и `lastRowId` помогают анализировать результаты выполнения запросов.
- Функция `upgradeSchema` позволяет обновлять схему базы данных.

Этот модуль подходит для задач, таких как хранение данных, управление схемой базы данных и выполнение сложных SQL-запросов.
