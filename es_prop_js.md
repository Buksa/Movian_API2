# Prop Module Functions

Модуль `prop` предоставляет функции для работы с свойствами (properties) в ECMAScript. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`prop.print(prop)`**

- **Описание**: Выводит дерево свойств в консоль.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.print(myProp);
    ```

### 2. **`prop.release(prop)`**

- **Описание**: Освобождает ресурсы, связанные с объектом свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.release(myProp);
    ```

### 3. **`prop.create(name)`**

- **Описание**: Создает новое свойство с указанным именем.
- **Параметры**:
  - `name` (`string`): Имя свойства
- **Возвращаемое значение**: `Object` - Созданное свойство
- **Пример**:
    ```js
    var newProp = prop.create('myProp');
    ```

### 4. **`prop.getValue(prop)`**

- **Описание**: Возвращает значение свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Возвращаемое значение**: `string`|`number`|`null` - Значение свойства
- **Пример**:
    ```js
    var value = prop.getValue(myProp);
    console.log('Value:', value);
    ```

### 5. **`prop.getName(prop)`**

- **Описание**: Возвращает имя свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Возвращаемое значение**: `string` - Имя свойства
- **Пример**:
    ```js
    var name = prop.getName(myProp);
    console.log('Name:', name);
    ```

### 6. **`prop.getChild(prop, key)`**

- **Описание**: Возвращает дочернее свойство по ключу или индексу.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `key` (`string`|`number`): Ключ или индекс дочернего свойства
- **Возвращаемое значение**: `Object` - Дочернее свойство или `null`
- **Пример**:
    ```js
    var childProp = prop.getChild(myProp, 'childKey');
    ```

### 7. **`prop.set(prop, key, value)`**

- **Описание**: Устанавливает значение свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `key` (`string`): Ключ свойства
  - `value` (`string`|`number`|`boolean`): Значение свойства
- **Пример**:
    ```js
    prop.set(myProp, 'key', 'value');
    ```

### 8. **`prop.setRichStr(prop, key, richStr)`**

- **Описание**: Устанавливает форматированную строку в свойство.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `key` (`string`): Ключ свойства
  - `richStr` (`string`): Форматированная строка
- **Пример**:
    ```js
    prop.setRichStr(myProp, 'key', '<b>Rich text</b>');
    ```

### 9. **`prop.setParent(prop, parent)`**

- **Описание**: Устанавливает родительское свойство.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `parent` (`Object`): Родительское свойство
- **Пример**:
    ```js
    prop.setParent(childProp, parentProp);
    ```

### 10. **`prop.subscribe(prop, callback, options)`**

- **Описание**: Подписывается на изменения свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `callback` (`function`): Функция обратного вызова
  - `options` (`Object`): Опции подписки:
    - `autoDestroy` (`boolean`): Автоматически уничтожать подписку при уничтожении свойства
    - `ignoreVoid` (`boolean`): Игнорировать события с пустыми значениями
    - `debug` (`boolean`): Включить отладку
    - `noInitialUpdate` (`boolean`): Не отправлять начальное обновление
    - `earlyChildDelete` (`boolean`): Раннее удаление дочерних свойств
    - `actionAsArray` (`boolean`): Возвращать действия как массив
- **Пример**:
    ```js
    prop.subscribe(myProp, function(event, value) {
      console.log('Property changed:', value);
    }, { autoDestroy: true });
    ```

### 11. **`prop.haveMore(prop, yes)`**

- **Описание**: Указывает, что свойство имеет больше дочерних элементов.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `yes` (`boolean`): Указывает, есть ли больше дочерних элементов
- **Пример**:
    ```js
    prop.haveMore(myProp, true);
    ```

### 12. **`prop.makeUrl(prop)`**

- **Описание**: Создает URL для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Возвращаемое значение**: `string` - URL
- **Пример**:
    ```js
    var url = prop.makeUrl(myProp);
    console.log('URL:', url);
    ```

### 13. **`prop.global()`**

- **Описание**: Возвращает глобальное свойство.
- **Возвращаемое значение**: `Object` - Глобальное свойство
- **Пример**:
    ```js
    var globalProp = prop.global();
    ```

### 14. **`prop.enumerate(prop)`**

- **Описание**: Возвращает массив имен дочерних свойств.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Возвращаемое значение**: `Array` - Массив имен дочерних свойств
- **Пример**:
    ```js
    var childNames = prop.enumerate(myProp);
    console.log('Child names:', childNames);
    ```

### 15. **`prop.has(prop, key)`**

- **Описание**: Проверяет наличие дочернего свойства по ключу.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `key` (`string`): Ключ дочернего свойства
- **Возвращаемое значение**: `boolean` - Наличие свойства
- **Пример**:
    ```js
    var hasChild = prop.has(myProp, 'childKey');
    console.log('Has child:', hasChild);
    ```

### 16. **`prop.deleteChild(prop, key)`**

- **Описание**: Удаляет дочернее свойство по ключу.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `key` (`string`): Ключ дочернего свойства
- **Пример**:
    ```js
    prop.deleteChild(myProp, 'childKey');
    ```

### 17. **`prop.deleteChilds(prop)`**

- **Описание**: Удаляет все дочерние свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.deleteChilds(myProp);
    ```

### 18. **`prop.destroy(prop)`**

- **Описание**: Уничтожает свойство.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.destroy(myProp);
    ```

### 19. **`prop.select(prop)`**

- **Описание**: Выбирает свойство.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.select(myProp);
    ```

### 20. **`prop.link(prop, parent)`**

- **Описание**: Связывает свойство с родительским свойством.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `parent` (`Object`): Родительское свойство
- **Пример**:
    ```js
    prop.link(childProp, parentProp);
    ```

### 21. **`prop.unlink(prop)`**

- **Описание**: Отвязывает свойство от родительского свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.unlink(myProp);
    ```

### 22. **`prop.sendEvent(prop, type, args)`**

- **Описание**: Отправляет событие для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `type` (`string`): Тип события (`"redirect"`, `"openurl"`)
  - `args` (`Object`): Аргументы события
- **Пример**:
    ```js
    prop.sendEvent(myProp, 'redirect', { url: 'https://example.com' });
    ```

### 23. **`prop.isValue(prop)`**

- **Описание**: Проверяет, является ли свойство значением (не директорией).
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Возвращаемое значение**: `boolean` - Является ли свойство значением
- **Пример**:
    ```js
    var isValue = prop.isValue(myProp);
    console.log('Is value:', isValue);
    ```

### 24. **`prop.atomicAdd(prop, num)`**

- **Описание**: Атомарно добавляет число к значению свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `num` (`number`): Число для добавления
- **Пример**:
    ```js
    prop.atomicAdd(myProp, 5);
    ```

### 25. **`prop.isSame(prop1, prop2)`**

- **Описание**: Проверяет, являются ли два свойства одинаковыми.
- **Параметры**:
  - `prop1` (`Object`): Первое свойство
  - `prop2` (`Object`): Второе свойство
- **Возвращаемое значение**: `boolean` - Являются ли свойства одинаковыми
- **Пример**:
    ```js
    var isSame = prop.isSame(prop1, prop2);
    console.log('Is same:', isSame);
    ```

### 26. **`prop.moveBefore(prop, beforeProp)`**

- **Описание**: Перемещает свойство перед другим свойством.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `beforeProp` (`Object`): Свойство, перед которым нужно переместить
- **Пример**:
    ```js
    prop.moveBefore(prop1, prop2);
    ```

### 27. **`prop.unloadDestroy(prop)`**

- **Описание**: Уничтожает свойство при выгрузке контекста.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Пример**:
    ```js
    prop.unloadDestroy(myProp);
    ```

### 28. **`prop.isZombie(prop)`**

- **Описание**: Проверяет, является ли свойство "зомби" (уничтоженным).
- **Параметры**:
  - `prop` (`Object`): Объект свойства
- **Возвращаемое значение**: `boolean` - Является ли свойство "зомби"
- **Пример**:
    ```js
    var isZombie = prop.isZombie(myProp);
    console.log('Is zombie:', isZombie);
    ```

### 29. **`prop.setClipRange(prop, start, end)`**

- **Описание**: Устанавливает диапазон обрезки для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `start` (`number`): Начало диапазона
  - `end` (`number`): Конец диапазона
- **Пример**:
    ```js
    prop.setClipRange(myProp, 0, 100);
    ```

### 30. **`prop.tagSet(prop, tag, value)`**

- **Описание**: Устанавливает тег для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `tag` (`Object`): Тег
  - `value` (`Object`): Значение тега
- **Пример**:
    ```js
    prop.tagSet(myProp, tag, value);
    ```

### 31. **`prop.tagClear(prop, tag)`**

- **Описание**: Очищает тег для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `tag` (`Object`): Тег
- **Пример**:
    ```js
    prop.tagClear(myProp, tag);
    ```

### 32. **`prop.tagGet(prop, tag)`**

- **Описание**: Возвращает значение тега для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `tag` (`Object`): Тег
- **Возвращаемое значение**: `Object` - Значение тега
- **Пример**:
    ```js
    var tagValue = prop.tagGet(myProp, tag);
    console.log('Tag value:', tagValue);
    ```

### 33. **`prop.nodeFilterCreate(prop, filter)`**

- **Описание**: Создает фильтр узлов для свойства.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `filter` (`Object`): Фильтр
- **Возвращаемое значение**: `Object` - Фильтр узлов
- **Пример**:
    ```js
    var nodeFilter = prop.nodeFilterCreate(myProp, filter);
    ```

### 34. **`prop.nodeFilterAddPred(nodeFilter, path, cmp, value, enable, mode)`**

- **Описание**: Добавляет предикат в фильтр узлов.
- **Параметры**:
  - `nodeFilter` (`Object`): Фильтр узлов
  - `path` (`string`): Путь
  - `cmp` (`string`): Функция сравнения (`"eq"`, `"neq"`)
  - `value` (`string`|`number`): Значение для сравнения
  - `enable` (`Object`): Свойство для включения/выключения
  - `mode` (`string`): Режим фильтра (`"include"`, `"exclude"`)
- **Возвращаемое значение**: `number` - Идентификатор предиката
- **Пример**:
    ```js
    var predId = prop.nodeFilterAddPred(nodeFilter, 'path', 'eq', 'value', enableProp, 'include');
    ```

### 35. **`prop.nodeFilterDelPred(nodeFilter, predId)`**

- **Описание**: Удаляет предикат из фильтра узлов.
- **Параметры**:
  - `nodeFilter` (`Object`): Фильтр узлов
  - `predId` (`number`): Идентификатор предиката
- **Пример**:
    ```js
    prop.nodeFilterDelPred(nodeFilter, predId);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля prop

// Создание свойства
var myProp = prop.create('myProp');

// Установка значения
prop.set(myProp, 'key', 'value');

// Получение значения
var value = prop.getValue(myProp);
console.log('Value:', value);

// Подписка на изменения
prop.subscribe(myProp, function(event, value) {
  console.log('Property changed:', value);
}, { autoDestroy: true });

// Уничтожение свойства
prop.destroy(myProp);
