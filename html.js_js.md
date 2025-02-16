# HTML Module Functions

Модуль `html` предоставляет функции для работы с HTML документами. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`html.parse(html)`**

- **Описание**: Парсит HTML строку и возвращает объект документа.
- **Параметры**:
  - `html` (`string`): HTML строка для парсинга
- **Возвращаемое значение**: `Object` - Объект документа. Свойства:
  - `document` (`Object`): Корневой узел документа
  - `root` (`Object`): Корневой элемент HTML
- **Пример**:
    ```js
    var html = '<html><body><div id="content">Hello</div></body></html>';
    var doc = html.parse(html);
    console.log('Document:', doc);
    ```

### 2. **NodeProto.prototype Properties**

#### `node.nodeName`
- **Описание**: Возвращает имя узла.
- **Возвращаемое значение**: `string` - Имя узла
- **Пример**:
    ```js
    var node = doc.document;
    console.log('Node name:', node.nodeName);
    ```

#### `node.nodeType`
- **Описание**: Возвращает тип узла.
- **Возвращаемое значение**: `number` - Тип узла:
  - 1: Элемент
  - 3: Текст
  - 8: Комментарий
  - 9: Документ
- **Пример**:
    ```js
    console.log('Node type:', node.nodeType);
    ```

#### `node.children`
- **Описание**: Возвращает дочерние узлы.
- **Возвращаемое значение**: `Array` - Массив дочерних узлов
- **Пример**:
    ```js
    var children = node.children;
    console.log('Children:', children);
    ```

#### `node.textContent`
- **Описание**: Возвращает текстовое содержимое узла.
- **Возвращаемое значение**: `string` - Текстовое содержимое
- **Пример**:
    ```js
    var text = node.textContent;
    console.log('Text content:', text);
    ```

#### `node.attributes`
- **Описание**: Возвращает атрибуты узла.
- **Возвращаемое значение**: `Array` - Массив атрибутов. Каждый атрибут:
  - `name` (`string`): Имя атрибута
  - `value` (`string`): Значение атрибута
- **Пример**:
    ```js
    var attrs = node.attributes;
    console.log('Attributes:', attrs);
    ```


### 3. **NodeProto.prototype Methods**

#### `node.getElementById(id)`
- **Описание**: Находит узел по идентификатору.
- **Параметры**:
  - `id` (`string`): Идентификатор элемента
- **Возвращаемое значение**: `Object` - Найденный узел или null
- **Пример**:
    ```js
    var elem = node.getElementById('content');
    console.log('Found element:', elem);
    ```

#### `node.getElementByClassName(className)`
- **Описание**: Находит узлы по имени класса.
- **Параметры**:
  - `className` (`string`): Имя класса
- **Возвращаемое значение**: `Array` - Массив найденных узлов
- **Пример**:
    ```js
    var elems = node.getElementByClassName('my-class');
    console.log('Elements with class:', elems);
    ```

#### `node.getElementByTagName(tag)`
- **Описание**: Находит узлы по имени тега.
- **Параметры**:
  - `tag` (`string`): Имя тега
- **Возвращаемое значение**: `Array` - Массив найденных узлов
- **Пример**:
    ```js
    var divs = node.getElementByTagName('div');
    console.log('Div elements:', divs);
    ```


### 7. **`node.getElementById(id)`**

- **Описание**: Находит узел по идентификатору.
- **Параметры**:
  - `id` (`string`): Идентификатор элемента
- **Возвращаемое значение**: `Object` - Найденный узел или null
- **Пример**:
    ```js
    var elem = node.getElementById('content');
    console.log('Found element:', elem);
    ```

### 8. **`node.getElementByClassName(className)`**

- **Описание**: Находит узлы по имени класса.
- **Параметры**:
  - `className` (`string`): Имя класса
- **Возвращаемое значение**: `Array` - Массив найденных узлов
- **Пример**:
    ```js
    var elems = node.getElementByClassName('my-class');
    console.log('Elements with class:', elems);
    ```

### 9. **`node.getElementByTagName(tag)`**

- **Описание**: Находит узлы по имени тега.
- **Параметры**:
  - `tag` (`string`): Имя тега
- **Возвращаемое значение**: `Array` - Массив найденных узлов
- **Пример**:
    ```js
    var divs = node.getElementByTagName('div');
    console.log('Div elements:', divs);
    ```

## Рекомендации по использованию

1. **Управление памятью**:
   - Всегда освобождайте ресурсы после использования
   - Проверяйте возвращаемые значения функций
   - Используйте try/catch для обработки ошибок

2. **Производительность**:
   - Избегайте глубокого рекурсивного обхода больших документов
   - Используйте поиск по идентификатору вместо полного обхода
   - Кэшируйте часто используемые узлы

3. **Безопасность**:
   - Проверяйте входные данные перед парсингом
   - Ограничивайте размер обрабатываемых документов
   - Используйте санитизацию для недоверенных данных

4. **Обработка ошибок**:
   - Проверяйте возвращаемые значения функций
   - Обрабатывайте исключения
   - Используйте try/catch для критических операций
