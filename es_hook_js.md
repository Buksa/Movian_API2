# Hook Module Functions

Модуль `hook` предоставляет функции для работы с хуками. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`hook.register(type, callback)`**

- **Описание**: Регистрирует хук для указанного типа событий.
- **Параметры**:
  - `type` (`string`): Тип события
  - `callback` (`function`): Функция обратного вызова
- **Возвращаемое значение**: `Object` - Объект хука
- **Пример**:
    ```js
    var myHook = hook.register('myEvent', function() {
      console.log('Event triggered');
    });
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля hook

// Регистрация хука для события 'myEvent'
var myHook = hook.register('myEvent', function() {
  console.log('Event triggered');
});

// Пример вызова хука
hook.invoke('myEvent', function(ctx) {
  duk_push_string(ctx, 'Hello from hook');
  return 1;
});
