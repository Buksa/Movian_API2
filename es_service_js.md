# Service Module Functions

Модуль `service` предоставляет функции для работы с сервисами. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`service.create(id, title, url, type, enabled, icon)`**

- **Описание**: Создает новый сервис.
- **Параметры**:
  - `id` (`string`): Идентификатор сервиса
  - `title` (`string`): Название сервиса
  - `url` (`string`): URL сервиса
  - `type` (`string`): Тип сервиса
  - `enabled` (`boolean`): Включен ли сервис
  - `icon` (`string`): Иконка сервиса (опционально)
- **Возвращаемое значение**: `Object` - Созданный сервис
- **Пример**:
    ```js
    var myService = service.create('myService', 'My Service', 'https://example.com', 'web', true, 'icon.png');
    ```

### 2. **`service.enable(service, enabled)`**

- **Описание**: Включает или отключает сервис.
- **Параметры**:
  - `service` (`Object`): Объект сервиса
  - `enabled` (`boolean`): Включить или отключить сервис
- **Пример**:
    ```js
    service.enable(myService, false); // Отключить сервис
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля service

// Создание сервиса
var myService = service.create('myService', 'My Service', 'https://example.com', 'web', true, 'icon.png');

// Отключение сервиса
service.enable(myService, false);
