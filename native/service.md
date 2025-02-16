# Документация модуля `service`

Модуль `service` предоставляет функции для создания и управления сервисами в системе. Сервисы могут представлять собой различные внешние или внутренние службы, такие как плагины, веб-сервисы или другие ресурсы. Этот модуль позволяет создавать сервисы, управлять их состоянием (включено/выключено) и выполнять действия, такие как удаление или отключение сервисов.

---

## Основные функции

### 1. `create(id, title, url, type, enabled, icon)`
Создает новый сервис.

- **Аргументы**:
  - `id` (строка): Уникальный идентификатор сервиса.
  - `title` (строка): Название сервиса.
  - `url` (строка): URL сервиса.
  - `type` (строка): Тип сервиса.
  - `enabled` (булево): Состояние сервиса (включен/выключен).
  - `icon` (строка, опционально): Иконка сервиса.
- **Возвращает**: Объект сервиса.
- **Пример**:
  ```javascript
  var service = require('service');
  var myService = service.create('myService', 'My Service', 'https://example.com', 'web', true, 'icon.png');
  ```

---

### 2. `enable(service, enabled)`
Включает или выключает сервис.

- **Аргументы**:
  - `service` (объект): Объект сервиса.
  - `enabled` (булево, опционально): Новое состояние сервиса (включен/выключен). Если не указано, возвращает текущее состояние.
- **Возвращает**: Текущее состояние сервиса, если `enabled` не указано.
- **Пример**:
  ```javascript
  var service = require('service');
  var myService = service.create('myService', 'My Service', 'https://example.com', 'web', true, 'icon.png');

  // Включение сервиса
  service.enable(myService, true);

  // Получение текущего состояния
  var isEnabled = service.enable(myService);
  console.log('Сервис включен:', isEnabled);
  ```

---

## Пример использования

### Создание и управление сервисом

```javascript
var service = require('service');

// Создание сервиса
var myService = service.create(
  'myService',              // Идентификатор
  'My Service',             // Название
  'https://example.com',    // URL
  'web',                    // Тип
  true,                     // Включен
  'icon.png'                // Иконка
);

// Включение/выключение сервиса
service.enable(myService, false); // Выключить сервис
service.enable(myService, true);  // Включить сервис

// Получение текущего состояния
var isEnabled = service.enable(myService);
console.log('Сервис включен:', isEnabled);
```

---

### Удаление сервиса (для плагинов)

Если сервис связан с плагином, можно добавить возможность его удаления:

```javascript
var service = require('service');

// Создание сервиса для плагина
var pluginService = service.create(
  'pluginService',          // Идентификатор
  'My Plugin',              // Название
  'https://example.com',    // URL
  'plugin',                 // Тип
  true,                     // Включен
  'plugin-icon.png'         // Иконка
);

// Установка текста для кнопки удаления
prop.set(pluginService.s_root, 'deleteText', 'Uninstall');

// Обработка запроса на удаление
prop.subscribe(pluginService.s_root, { autoDestroy: true }, function(event) {
  if (event === 'delete') {
    console.log('Плагин удален');
    // Дополнительная логика для удаления плагина
  }
});
```

---

## Примечания

- Модуль `service` позволяет создавать и управлять сервисами, такими как плагины или веб-сервисы.
- Используйте функцию `create` для создания сервиса и `enable` для управления его состоянием.
- Для сервисов, связанных с плагинами, можно добавить возможность удаления через подписку на события.

Этот модуль подходит для задач, таких как управление плагинами, интеграция с внешними сервисами и контроль состояния ресурсов.
