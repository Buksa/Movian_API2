Вот обновленный Markdown файл с дополнительными примерами использования функций модуля SQLite на русском языке с синтаксисом ES5.1:

---

# Документация модуля SQLite

Этот модуль предоставляет интерфейс для работы с базами данных SQLite в JavaScript-окружении с использованием движка Duktape. Он позволяет создавать базы данных, выполнять запросы и управлять транзакциями.

---

## Содержание
1. [Функции](#функции)
   - [`create(name)`](#createname)
   - [`query(sql, ...args)`](#querysql-args)
   - [`step()`](#step)
   - [`changes()`](#changes)
   - [`lastErrorCode()`](#lasterrorcode)
   - [`lastErrorString()`](#lasterrorstring)
   - [`lastRowId()`](#lastrowid)
   - [`upgradeSchema(sql, version)`](#upgradeschemasql-version)
2. [Примеры](#примеры)
   - [Создание базы данных и таблицы](#создание-базы-данных-и-таблицы)
   - [Вставка и выборка данных](#вставка-и-выборка-данных)
   - [Обновление данных](#обновление-данных)
   - [Удаление данных](#удаление-данных)
   - [Обработка ошибок](#обработка-ошибок)
   - [Обновление схемы](#обновление-схемы)
   - [Работа с транзакциями](#работа-с-транзакциями)

---

## Функции

### `create(name)`
Создает новую базу данных SQLite с указанным именем. База данных сохраняется в директории, связанной с текущим контекстом (плагином).

**Параметры:**
- `name` (строка) — Имя базы данных.

**Возвращает:**
Объект базы данных, который можно использовать для выполнения запросов.

**Пример:**
```javascript
var db = sqlite.create("my_database");
```

---

### `query(sql, ...args)`
Выполняет SQL-запрос с возможностью передачи параметров. Поддерживает подготовленные выражения для безопасной передачи данных.

**Параметры:**
- `sql` (строка) — SQL-запрос.
- `...args` (опционально) — Параметры для запроса.

**Возвращает:**
Ничего. Для получения результатов используйте функцию `step`.

**Пример:**
```javascript
db.query("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)");
db.query("INSERT INTO users (name) VALUES (?)", "Alice");
db.query("INSERT INTO users (name) VALUES (?)", "Bob");
```

---

### `step()`
Выполняет шаг выполнения запроса и возвращает текущую строку результата в виде объекта. Если строк больше нет, возвращает `null`.

**Возвращает:**
- Объект, представляющий текущую строку результата, или `null`, если строк больше нет.

**Пример:**
```javascript
db.query("SELECT * FROM users");
var row;
while ((row = db.step()) !== null) {
    console.log(row.id, row.name); // Вывод: 1 Alice, 2 Bob
}
```

---

### `changes()`
Возвращает количество строк, измененных последним запросом (например, `INSERT`, `UPDATE`, `DELETE`).

**Возвращает:**
Количество измененных строк.

**Пример:**
```javascript
db.query("DELETE FROM users WHERE name = ?", "Alice");
var deletedCount = db.changes();
console.log("Удалено строк: " + deletedCount); // Вывод: Удалено строк: 1
```

---

### `lastErrorCode()`
Возвращает код последней ошибки, произошедшей при выполнении запроса.

**Возвращает:**
Числовой код ошибки SQLite.

**Пример:**
```javascript
try {
    db.query("INVALID SQL");
} catch (e) {
    var errorCode = db.lastErrorCode();
    console.log("Код ошибки SQLite: " + errorCode);
}
```

---

### `lastErrorString()`
Возвращает текстовое описание последней ошибки, произошедшей при выполнении запроса.

**Возвращает:**
Строку с описанием ошибки.

**Пример:**
```javascript
try {
    db.query("INVALID SQL");
} catch (e) {
    var errorMessage = db.lastErrorString();
    console.log("Ошибка: " + errorMessage);
}
```

---

### `lastRowId()`
Возвращает идентификатор последней вставленной строки.

**Возвращает:**
Идентификатор строки в виде числа.

**Пример:**
```javascript
db.query("INSERT INTO users (name) VALUES (?)", "Charlie");
var lastId = db.lastRowId();
console.log("Последний ID: " + lastId); // Вывод: Последний ID: 3
```

---

### `upgradeSchema(sql, version)`
Обновляет схему базы данных до указанной версии. Используется для миграций.

**Параметры:**
- `sql` (строка) — SQL-запрос для обновления схемы.
- `version` (число) — Версия схемы.

**Пример:**
```javascript
db.upgradeSchema(
    "CREATE TABLE IF NOT EXISTS settings (" +
    "key TEXT PRIMARY KEY, " +
    "value TEXT" +
    ");",
    1
);
```

---

## Примеры

### Создание базы данных и таблицы
```javascript
var db = sqlite.create("my_database");
db.query("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)");
```

### Вставка и выборка данных
```javascript
db.query("INSERT INTO users (name) VALUES (?)", "Alice");
db.query("INSERT INTO users (name) VALUES (?)", "Bob");

db.query("SELECT * FROM users");
var row;
while ((row = db.step()) !== null) {
    console.log(row.id, row.name); // Вывод: 1 Alice, 2 Bob
}
```

### Обновление данных
```javascript
db.query("UPDATE users SET name = ? WHERE id = ?", "Alicia", 1);
var updatedCount = db.changes();
console.log("Обновлено строк: " + updatedCount); // Вывод: Обновлено строк: 1
```

### Удаление данных
```javascript
db.query("DELETE FROM users WHERE name = ?", "Bob");
var deletedCount = db.changes();
console.log("Удалено строк: " + deletedCount); // Вывод: Удалено строк: 1
```

### Обработка ошибок
```javascript
try {
    db.query("INVALID SQL");
} catch (e) {
    console.log("Ошибка: " + db.lastErrorString()); // Вывод: Ошибка: near "INVALID": syntax error
}
```

### Обновление схемы
```javascript
db.upgradeSchema(
    "CREATE TABLE IF NOT EXISTS settings (" +
    "key TEXT PRIMARY KEY, " +
    "value TEXT" +
    ");",
    1
);
```

### Работа с транзакциями
```javascript
try {
    db.query("BEGIN TRANSACTION");
    db.query("INSERT INTO users (name) VALUES (?)", "David");
    db.query("INSERT INTO users (name) VALUES (?)", "Eve");
    db.query("COMMIT");
} catch (e) {
    db.query("ROLLBACK");
    console.log("Транзакция отменена: " + db.lastErrorString());
}
```

---

Этот Markdown файл содержит подробное описание функций модуля SQLite, их параметры, возвращаемые значения и множество примеров использования на ES5.1.
