# Timer Module Functions

Модуль `timer` предоставляет функции для работы с таймерами, включая установку таймеров и интервалов. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`timer.setTimeout(callback, delay)`**

- **Описание**: Устанавливает таймер, который вызывает функцию `callback` через указанное количество миллисекунд.
- **Параметры**:
  - `callback` (`function`): Функция, которая будет вызвана
  - `delay` (`number`): Задержка в миллисекундах
- **Возвращаемое значение**: `Object` - Объект таймера
- **Пример**:
    ```js
    timer.setTimeout(function() {
      console.log('Timeout executed');
    }, 1000);
    ```

### 2. **`timer.setInterval(callback, interval)`**

- **Описание**: Устанавливает интервал, который вызывает функцию `callback` через указанное количество миллисекунд.
- **Параметры**:
  - `callback` (`function`): Функция, которая будет вызвана
  - `interval` (`number`): Интервал в миллисекундах
- **Возвращаемое значение**: `Object` - Объект интервала
- **Пример**:
    ```js
    timer.setInterval(function() {
      console.log('Interval executed');
    }, 1000);
    ```

### 3. **`timer.clearTimeout(timer)`**

- **Описание**: Останавливает таймер.
- **Параметры**:
  - `timer` (`Object`): Объект таймера, возвращенный `setTimeout`
- **Пример**:
    ```js
    var myTimer = timer.setTimeout(function() {
      console.log('Timeout executed');
    }, 1000);
    timer.clearTimeout(myTimer);
    ```

### 4. **`timer.clearInterval(interval)`**

- **Описание**: Останавливает интервал.
- **Параметры**:
  - `interval` (`Object`): Объект интервала, возвращенный `setInterval`
- **Пример**:
    ```js
    var myInterval = timer.setInterval(function() {
      console.log('Interval executed');
    }, 1000);
    timer.clearInterval(myInterval);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля timer

// Установка таймера
var myTimer = timer.setTimeout(function() {
  console.log('Timeout executed');
}, 1000);

// Установка интервала
var myInterval = timer.setInterval(function() {
  console.log('Interval executed');
}, 1000);

// Остановка таймера
timer.clearTimeout(myTimer);

// Остановка интервала
timer.clearInterval(myInterval);
