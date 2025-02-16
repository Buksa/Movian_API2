# Документация модуля `prop`

Модуль `prop` предоставляет функции для работы с объектами свойств (properties) в системе. Эти объекты используются для представления иерархических данных, таких как настройки, состояния и другие структурированные данные. Модуль позволяет создавать, изменять, подписываться на изменения и управлять свойствами.

---

## Основные функции

### 1. `print()`
Выводит дерево свойств в консоль.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.print(myProp);
  ```

---

### 2. `release()`
Освобождает ресурсы, связанные с объектом свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.release(myProp);
  ```

---

### 3. `create(name)`
Создает новый объект свойства с указанным именем.

- **Аргументы**:
  - `name` (строка): Имя свойства.
- **Возвращает**: Новый объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var newProp = prop.create('myProperty');
  ```

---

### 4. `getValue()`
Возвращает значение свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Возвращает**: Значение свойства (строка, число, булево или `null`).
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var value = prop.getValue(myProp);
  console.log('Значение:', value);
  ```

---

### 5. `getName()`
Возвращает имя свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Возвращает**: Имя свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var name = prop.getName(myProp);
  console.log('Имя свойства:', name);
  ```

---

### 6. `getChild(nameOrIndex)`
Возвращает дочернее свойство по имени или индексу.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `nameOrIndex` (строка или число): Имя или индекс дочернего свойства.
- **Возвращает**: Дочерний объект свойства или `undefined`, если не найден.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var childProp = prop.getChild(myProp, 'childName');
  ```

---

### 7. `set(name, value)`
Устанавливает значение свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `name` (строка): Имя свойства.
  - `value` (строка, число, булево или `null`): Значение для установки.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.set(myProp, 'myKey', 'myValue');
  ```

---

### 8. `setRichStr(name, richStr)`
Устанавливает форматированную строку в качестве значения свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `name` (строка): Имя свойства.
  - `richStr` (строка): Форматированная строка.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.setRichStr(myProp, 'myKey', '<b>Formatted Text</b>');
  ```

---

### 9. `setParent(parent)`
Устанавливает родительское свойство для текущего свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `parent` (объект): Родительский объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.setParent(myProp, parentProp);
  ```

---

### 10. `subscribe(options, callback)`
Подписывается на изменения свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `options` (объект): Опции подписки:
    - `autoDestroy` (булево): Автоматически уничтожать подписку при уничтожении свойства.
    - `ignoreVoid` (булево): Игнорировать пустые значения.
    - `debug` (булево): Включить отладку.
    - `noInitialUpdate` (булево): Не отправлять начальное обновление.
    - `earlyChildDelete` (булево): Раннее удаление дочерних элементов.
    - `actionAsArray` (булево): Возвращать действия как массив.
  - `callback` (функция): Функция обратного вызова для обработки изменений.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.subscribe(myProp, { autoDestroy: true }, function(event, value) {
    console.log('Событие:', event, 'Значение:', value);
  });
  ```

---

### 11. `haveMore(hasMore)`
Указывает, есть ли у свойства дополнительные дочерние элементы.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `hasMore` (булево): `true`, если есть дополнительные дочерние элементы.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.haveMore(myProp, true);
  ```

---

### 12. `makeUrl()`
Создает URL для свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Возвращает**: URL в виде строки.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var url = prop.makeUrl(myProp);
  console.log('URL:', url);
  ```

---

### 13. `global()`
Возвращает глобальный объект свойства.

- **Возвращает**: Глобальный объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var globalProp = prop.global();
  ```

---

### 14. `enumerate()`
Возвращает массив имен дочерних свойств.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Возвращает**: Массив имен дочерних свойств.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var childNames = prop.enumerate(myProp);
  console.log('Дочерние свойства:', childNames);
  ```

---

### 15. `has(name)`
Проверяет, существует ли дочернее свойство с указанным именем.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `name` (строка): Имя дочернего свойства.
- **Возвращает**: `true`, если свойство существует, иначе `false`.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var hasChild = prop.has(myProp, 'childName');
  console.log('Свойство существует:', hasChild);
  ```

---

### 16. `deleteChild(name)`
Удаляет дочернее свойство по имени.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `name` (строка): Имя дочернего свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.deleteChild(myProp, 'childName');
  ```

---

### 17. `deleteChilds()`
Удаляет все дочерние свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.deleteChilds(myProp);
  ```

---

### 18. `destroy()`
Уничтожает объект свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.destroy(myProp);
  ```

---

### 19. `select()`
Выбирает свойство для дальнейших операций.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.select(myProp);
  ```

---

### 20. `link(child)`
Связывает дочернее свойство с текущим.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `child` (объект): Дочерний объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.link(parentProp, childProp);
  ```

---

### 21. `unlink()`
Отсоединяет свойство от родительского.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.unlink(myProp);
  ```

---

### 22. `sendEvent(type, args)`
Отправляет событие, связанное с свойством.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `type` (строка): Тип события (`"redirect"`, `"openurl"`).
  - `args` (объект): Аргументы события.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.sendEvent(myProp, 'redirect', { url: 'https://example.com' });
  ```

---

### 23. `isValue()`
Проверяет, является ли свойство значением (строка, число, булево или `null`).

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Возвращает**: `true`, если свойство является значением, иначе `false`.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var isValue = prop.isValue(myProp);
  console.log('Свойство является значением:', isValue);
  ```

---

### 24. `atomicAdd(value)`
Атомарно добавляет значение к свойству.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `value` (число): Значение для добавления.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.atomicAdd(myProp, 10);
  ```

---

### 25. `isSame(otherProp)`
Проверяет, является ли свойство тем же объектом, что и `otherProp`.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `otherProp` (объект): Другой объект свойства.
- **Возвращает**: `true`, если свойства совпадают, иначе `false`.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var isSame = prop.isSame(myProp, otherProp);
  console.log('Свойства совпадают:', isSame);
  ```

---

### 26. `moveBefore(otherProp)`
Перемещает свойство перед другим свойством.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `otherProp` (объект): Другой объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.moveBefore(myProp, otherProp);
  ```

---

### 27. `unloadDestroy()`
Помечает свойство для уничтожения при выгрузке.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.unloadDestroy(myProp);
  ```

---

### 28. `isZombie()`
Проверяет, является ли свойство "зомби" (уничтоженным, но еще не удаленным).

- **Аргументы**:
  - `prop` (объект): Объект свойства.
- **Возвращает**: `true`, если свойство является "зомби", иначе `false`.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var isZombie = prop.isZombie(myProp);
  console.log('Свойство является зомби:', isZombie);
  ```

---

### 29. `setClipRange(min, max)`
Устанавливает диапазон значений для свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `min` (число): Минимальное значение.
  - `max` (число): Максимальное значение.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.setClipRange(myProp, 0, 100);
  ```

---

### 30. `tagSet(tag, value)`
Устанавливает тег для свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `tag` (строка): Имя тега.
  - `value` (любое): Значение тега.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.tagSet(myProp, 'myTag', 'myValue');
  ```

---

### 31. `tagClear(tag)`
Очищает тег свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `tag` (строка): Имя тега.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.tagClear(myProp, 'myTag');
  ```

---

### 32. `tagGet(tag)`
Возвращает значение тега свойства.

- **Аргументы**:
  - `prop` (объект): Объект свойства.
  - `tag` (строка): Имя тега.
- **Возвращает**: Значение тега или `undefined`, если тег не найден.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var tagValue = prop.tagGet(myProp, 'myTag');
  console.log('Значение тега:', tagValue);
  ```

---

### 33. `nodeFilterCreate(source, target)`
Создает фильтр узлов для свойств.

- **Аргументы**:
  - `source` (объект): Исходное свойство.
  - `target` (объект): Целевое свойство.
- **Возвращает**: Объект фильтра узлов.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  var filter = prop.nodeFilterCreate(sourceProp, targetProp);
  ```

---

### 34. `nodeFilterAddPred(filter, path, cmp, value, enable, mode)`
Добавляет предикат в фильтр узлов.

- **Аргументы**:
  - `filter` (объект): Объект фильтра узлов.
  - `path` (строка): Путь к свойству.
  - `cmp` (строка): Функция сравнения (`"eq"`, `"neq"`).
  - `value` (строка или число): Значение для сравнения.
  - `enable` (объект): Свойство для включения/выключения предиката.
  - `mode` (строка): Режим фильтрации (`"include"`, `"exclude"`).
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.nodeFilterAddPred(filter, 'myPath', 'eq', 'myValue', enableProp, 'include');
  ```

---

### 35. `nodeFilterDelPred(filter, predId)`
Удаляет предикат из фильтра узлов.

- **Аргументы**:
  - `filter` (объект): Объект фильтра узлов.
  - `predId` (число): Идентификатор предиката.
- **Пример**:
  ```javascript
  var prop = require('native/prop');
  prop.nodeFilterDelPred(filter, 1);
  ```

---

# Дополнительные примеры использования модуля `prop`

В этом разделе приведены дополнительные примеры использования модуля `prop` для различных задач, таких как создание иерархий свойств, управление событиями, фильтрация узлов и работа с тегами.

---

## Пример 1: Создание иерархии свойств

```javascript
var prop = require('native/prop');

// Создание корневого свойства
var rootProp = prop.create('root');

// Добавление дочерних свойств
var child1 = prop.create('child1');
var child2 = prop.create('child2');

// Установка значений дочерних свойств
prop.set(child1, 'name', 'Child 1');
prop.set(child2, 'name', 'Child 2');

// Связывание дочерних свойств с корневым
prop.setParent(child1, rootProp);
prop.setParent(child2, rootProp);

// Получение и вывод имен дочерних свойств
var childNames = prop.enumerate(rootProp);
console.log('Дочерние свойства:', childNames);

// Получение значения дочернего свойства
var child1Name = prop.getValue(prop.getChild(rootProp, 'child1'));
console.log('Имя первого дочернего свойства:', child1Name);
```

---

## Пример 2: Подписка на изменения свойства

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Подписка на изменения
prop.subscribe(myProp, { autoDestroy: true }, function(event, value) {
  console.log('Событие:', event, 'Значение:', value);
});

// Установка значения свойства (вызовет событие)
prop.set(myProp, 'myKey', 'myValue');

// Уничтожение свойства (вызовет событие "destroyed")
prop.destroy(myProp);
```

---

## Пример 3: Работа с событиями

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Отправка события "redirect"
prop.sendEvent(myProp, 'redirect', { url: 'https://example.com' });

// Отправка события "openurl"
prop.sendEvent(myProp, 'openurl', {
  url: 'https://example.com',
  view: 'default',
  how: 'replace',
  parenturl: 'https://parent.com'
});
```

---

## Пример 4: Фильтрация узлов

```javascript
var prop = require('native/prop');

// Создание исходного и целевого свойств
var sourceProp = prop.create('source');
var targetProp = prop.create('target');

// Создание фильтра узлов
var filter = prop.nodeFilterCreate(sourceProp, targetProp);

// Добавление предиката в фильтр
prop.nodeFilterAddPred(filter, 'myPath', 'eq', 'myValue', null, 'include');

// Удаление предиката из фильтра
prop.nodeFilterDelPred(filter, 1);
```

---

## Пример 5: Работа с тегами

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Установка тега
prop.tagSet(myProp, 'myTag', 'myValue');

// Получение значения тега
var tagValue = prop.tagGet(myProp, 'myTag');
console.log('Значение тега:', tagValue);

// Очистка тега
prop.tagClear(myProp, 'myTag');
```

---

## Пример 6: Атомарные операции

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Установка начального значения
prop.set(myProp, 'counter', 0);

// Атомарное увеличение значения
prop.atomicAdd(prop.getChild(myProp, 'counter'), 5);

// Получение нового значения
var counterValue = prop.getValue(prop.getChild(myProp, 'counter'));
console.log('Значение счетчика:', counterValue);
```

---

## Пример 7: Управление диапазоном значений

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Установка диапазона значений
prop.setClipRange(myProp, 0, 100);

// Установка значения в пределах диапазона
prop.set(myProp, 'value', 50);

// Попытка установить значение за пределами диапазона
prop.set(myProp, 'value', 150); // Значение будет ограничено 100
```

---

## Пример 8: Уничтожение свойств при выгрузке

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Помечение свойства для уничтожения при выгрузке
prop.unloadDestroy(myProp);

// Проверка, является ли свойство "зомби"
var isZombie = prop.isZombie(myProp);
console.log('Свойство является зомби:', isZombie);
```

---

## Пример 9: Перемещение свойств

```javascript
var prop = require('native/prop');

// Создание свойств
var parentProp = prop.create('parent');
var child1 = prop.create('child1');
var child2 = prop.create('child2');

// Связывание дочерних свойств с родительским
prop.setParent(child1, parentProp);
prop.setParent(child2, parentProp);

// Перемещение child1 перед child2
prop.moveBefore(child1, child2);

// Получение и вывод порядка дочерних свойств
var childNames = prop.enumerate(parentProp);
console.log('Порядок дочерних свойств:', childNames);
```

---

## Пример 10: Проверка типа свойства

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Установка значения
prop.set(myProp, 'myKey', 'myValue');

// Проверка, является ли свойство значением
var isValue = prop.isValue(myProp);
console.log('Свойство является значением:', isValue);

// Проверка, является ли свойство "зомби"
var isZombie = prop.isZombie(myProp);
console.log('Свойство является зомби:', isZombie);
```

---

## Пример 11: Создание и использование фильтров узлов

```javascript
var prop = require('native/prop');

// Создание исходного и целевого свойств
var sourceProp = prop.create('source');
var targetProp = prop.create('target');

// Создание фильтра узлов
var filter = prop.nodeFilterCreate(sourceProp, targetProp);

// Добавление предиката для включения узлов с определенным значением
prop.nodeFilterAddPred(filter, 'path.to.property', 'eq', 'desiredValue', null, 'include');

// Добавление предиката для исключения узлов с другим значением
prop.nodeFilterAddPred(filter, 'path.to.anotherProperty', 'neq', 'excludedValue', null, 'exclude');

// Удаление предиката по идентификатору
prop.nodeFilterDelPred(filter, 1);
```

---

## Пример 12: Использование тегов для хранения метаданных

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Установка тега с метаданными
prop.tagSet(myProp, 'metadata', { author: 'John Doe', version: 1.0 });

// Получение значения тега
var metadata = prop.tagGet(myProp, 'metadata');
console.log('Метаданные:', metadata);

// Очистка тега
prop.tagClear(myProp, 'metadata');
```

---

## Пример 13: Работа с глобальными свойствами

```javascript
var prop = require('native/prop');

// Получение глобального свойства
var globalProp = prop.global();

// Установка значения в глобальное свойство
prop.set(globalProp, 'globalKey', 'globalValue');

// Получение значения из глобального свойства
var globalValue = prop.getValue(prop.getChild(globalProp, 'globalKey'));
console.log('Глобальное значение:', globalValue);
```

---

## Пример 14: Управление дочерними свойствами

```javascript
var prop = require('native/prop');

// Создание родительского свойства
var parentProp = prop.create('parent');

// Добавление дочерних свойств
var child1 = prop.create('child1');
var child2 = prop.create('child2');

// Связывание дочерних свойств с родительским
prop.setParent(child1, parentProp);
prop.setParent(child2, parentProp);

// Удаление дочернего свойства
prop.deleteChild(parentProp, 'child1');

// Удаление всех дочерних свойств
prop.deleteChilds(parentProp);
```

---

## Пример 15: Использование форматированных строк

```javascript
var prop = require('native/prop');

// Создание свойства
var myProp = prop.create('myProperty');

// Установка форматированной строки
prop.setRichStr(myProp, 'formattedText', '<b>Hello, World!</b>');

// Получение значения свойства
var formattedText = prop.getValue(myProp);
console.log('Форматированный текст:', formattedText);
```

---

## Заключение

Модуль `prop` предоставляет мощные инструменты для работы с иерархическими данными, управления событиями, фильтрации узлов и хранения метаданных. Эти примеры демонстрируют, как можно использовать модуль для решения различных задач, таких как управление настройками, отслеживание состояний и работа с иерархическими структурами данных.
