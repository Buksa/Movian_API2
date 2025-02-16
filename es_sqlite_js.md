# SQLite Module Functions

Модуль `sqlite` предоставляет функции для работы с базами данных SQLite. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`sqlite.create(name)`**

- **Описание**: Создает новую базу данных SQLite или открывает существующую.
- **Параметры**:
  - `name` (`string`): Имя базы данных
- **Возвращаемое значение**: `Object` - Объект базы данных
- **Пример**:
    ```js
    var db = sqlite.create('myDatabase');
    ```

### 2. **`sqlite.query(db, query, ...args)`**

- **Описание**: Выполняет SQL-запрос в базе данных.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
  - `query` (`string`): SQL-запрос
  - `...args` (`any`): Аргументы для запроса
- **Пример**:
    ```js
    sqlite.query(db, 'INSERT INTO myTable (name) VALUES (?)', 'John');
    ```

### 3. **`sqlite.changes(db)`**

- **Описание**: Возвращает количество измененных строк в последнем запросе.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
- **Возвращаемое значение**: `number` - Количество измененных строк
- **Пример**:
    ```js
    var changes = sqlite.changes(db);
    console.log('Changes:', changes);
    ```

### 4. **`sqlite.step(db)`**

- **Описание**: Выполняет шаг выполнения запроса и возвращает следующую строку результата.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
- **Возвращаемое значение**: `Object` - Следующая строка результата или `null`, если строк больше нет
- **Пример**:
    ```js
    var row = sqlite.step(db);
    while(row !== null) {
      console.log('Row:', row);
      row = sqlite.step(db);
    }
    ```

### 5. **`sqlite.lastErrorCode(db)`**

- **Описание**: Возвращает код последней ошибки.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
- **Возвращаемое значение**: `number` - Код ошибки
- **Пример**:
    ```js
    var errorCode = sqlite.lastErrorCode(db);
    console.log('Error code:', errorCode);
    ```

### 6. **`sqlite.lastErrorString(db)`**

- **Описание**: Возвращает текстовое описание последней ошибки.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
- **Возвращаемое значение**: `string` - Описание ошибки
- **Пример**:
    ```js
    var errorString = sqlite.lastErrorString(db);
    console.log('Error:', errorString);
    ```

### 7. **`sqlite.lastRowId(db)`**

- **Описание**: Возвращает ID последней вставленной строки.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
- **Возвращаемое значение**: `number` - ID строки
- **Пример**:
    ```js
    var rowId = sqlite.lastRowId(db);
    console.log('Last row ID:', rowId);
    ```

### 8. **`sqlite.upgradeSchema(db, schema)`**

- **Описание**: Обновляет схему базы данных.
- **Параметры**:
  - `db` (`Object`): Объект базы данных
  - `schema` (`string`): Новая схема
- **Пример**:
    ```js
    sqlite.upgradeSchema(db, 'CREATE TABLE myTable (id INTEGER PRIMARY KEY, name TEXT)');
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля sqlite

// Создание базы данных
var db = sqlite.create('myDatabase');

// Создание таблицы
sqlite.query(db, 'CREATE TABLE IF NOT EXISTS myTable (id INTEGER PRIMARY KEY, name TEXT)');

// Вставка данных
sqlite.query(db, 'INSERT INTO myTable (name) VALUES (?)', 'John');

// Получение данных
sqlite.query(db, 'SELECT * FROM myTable');
var row = sqlite.step(db);
while(row !== null) {
  console.log('Row:', row);
  row = sqlite.step(db);
}

// Получение последнего ID
var lastId = sqlite.lastRowId(db);
console.log('Last row ID:', lastId);
