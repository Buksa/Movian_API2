# Core Module Functions

Модуль `Core` предоставляет базовые функции для работы с ECMAScript. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`Core.compile(path)`**

- **Описание**: Компилирует JavaScript код из указанного файла.
- **Параметры**:
  - `path` (`string`): Путь к файлу с JavaScript кодом
- **Возвращаемое значение**: `Function` - Скомпилированная функция
- **Пример**:
    ```js
    var func = Core.compile('/path/to/script.js');
    func();
    ```

### 2. **`Core.resourceDestroy(resource)`**

- **Описание**: Уничтожает указанный ресурс.
- **Параметры**:
  - `resource` (`Object`): Объект ресурса
- **Пример**:
    ```js
    Core.resourceDestroy(myResource);
    ```

### 3. **`Core.sleep(seconds)`**

- **Описание**: Приостанавливает выполнение на указанное количество секунд.
- **Параметры**:
  - `seconds` (`number`): Количество секунд для ожидания
- **Пример**:
    ```js
    Core.sleep(1.5); // Ожидание 1.5 секунды
    ```

### 4. **`Core.timestamp()`**

- **Описание**: Возвращает текущую временную метку в миллисекундах.
- **Возвращаемое значение**: `number` - Текущая временная метка
- **Пример**:
    ```js
    var ts = Core.timestamp();
    console.log('Current timestamp:', ts);
    ```

### 5. **`Core.randomBytes(length)`**

- **Описание**: Генерирует массив случайных байт указанной длины.
- **Параметры**:
  - `length` (`number`): Длина массива байт
- **Возвращаемое значение**: `Buffer` - Массив случайных байт
- **Пример**:
    ```js
    var bytes = Core.randomBytes(16);
    console.log('Random bytes:', bytes);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля Core

// Получение текущей временной метки
var ts = Core.timestamp();
console.log('Current timestamp:', ts);

// Генерация случайных байт
var randomBytes = Core.randomBytes(32);
console.log('Random bytes:', randomBytes);

// Ожидание 2 секунды
Core.sleep(2);

// Компиляция и выполнение скрипта
var func = Core.compile('/path/to/script.js');
func();
