# Gumbo Module Functions

Модуль `gumbo` предоставляет функции для работы с HTML документами. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`gumbo.parse(html)`**

- **Описание**: Парсит HTML строку и возвращает объект документа.
- **Параметры**:
  - `html` (`string`): HTML строка для парсинга
- **Возвращаемое значение**: `Object` - Объект документа с полями `document` и `root`
- **Пример**:
    ```js
    var doc = gumbo.parse('<html><body>Hello</body></html>');
    console.log('Document:', doc);
    ```

### 2. **`gumbo.nodeType(node)`**

- **Описание**: Возвращает тип узла.
- **Параметры**:
  - `node` (`Object`): Узел документа
- **Возвращаемое значение**: `number` - Тип узла:
    - 1: Элемент
    - 3: Текст
    - 8: Комментарий
    - 9: Документ
- **Пример**:
    ```js
    var type = gumbo.nodeType(node);
    console.log('Node type:', type);
    ```

### 3. **`gumbo.nodeName(node)`**

- **Описание**: Возвращает имя узла.
- **Параметры**:
  - `node` (`Object`): Узел документа
- **Возвращаемое значение**: `string` - Имя узла
- **Пример**:
    ```js
    var name = gumbo.nodeName(node);
    console.log('Node name:', name);
    ```

### 4. **`gumbo.nodeChilds(node, all)`**

- **Описание**: Возвращает дочерние узлы.
- **Параметры**:
  - `node` (`Object`): Узел документа
  - `all` (`boolean`): Включать текстовые узлы и комментарии
- **Возвращаемое значение**: `Array` - Массив дочерних узлов
- **Пример**:
    ```js
    var childs = gumbo.nodeChilds(node, true);
    console.log('Child nodes:', childs);
    ```

### 5. **`gumbo.nodeAttributes(node)`**

- **Описание**: Возвращает атрибуты узла.
- **Параметры**:
  - `node` (`Object`): Узел документа
- **Возвращаемое значение**: `Array` - Массив объектов атрибутов с полями `name` и `value`
- **Пример**:
    ```js
    var attrs = gumbo.nodeAttributes(node);
    console.log('Attributes:', attrs);
    ```

### 6. **`gumbo.nodeTextContent(node)`**

- **Описание**: Возвращает текстовое содержимое узла.
- **Параметры**:
  - `node` (`Object`): Узел документа
- **Возвращаемое значение**: `string` - Текстовое содержимое
- **Пример**:
    ```js
    var text = gumbo.nodeTextContent(node);
    console.log('Text content:', text);
    ```

### 7. **`gumbo.findById(node, id)`**

- **Описание**: Находит узел по идентификатору.
- **Параметры**:
  - `node` (`Object`): Узел документа
  - `id` (`string`): Идентификатор узла
- **Возвращаемое значение**: `Object` - Найденный узел или `undefined`
- **Пример**:
    ```js
    var node = gumbo.findById(doc.root, 'myId');
    console.log('Found node:', node);
    ```

### 8. **`gumbo.findByTagName(node, tag)`**

- **Описание**: Находит узлы по имени тега.
- **Параметры**:
  - `node` (`Object`): Узел документа
  - `tag` (`string`): Имя тега
- **Возвращаемое значение**: `Array` - Массив найденных узлов
- **Пример**:
    ```js
    var nodes = gumbo.findByTagName(doc.root, 'div');
    console.log('Found nodes:', nodes);
    ```

### 9. **`gumbo.findByClassName(node, className)`**

- **Описание**: Находит узлы по имени класса.
- **Параметры**:
  - `node` (`Object`): Узел документа
  - `className` (`string`): Имя класса
- **Возвращаемое значение**: `Array` - Массив найденных узлов
- **Пример**:
    ```js
    var nodes = gumbo.findByClassName(doc.root, 'myClass');
    console.log('Found nodes:', nodes);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля gumbo
var html = '<html><body><div id="main" class="content">Hello</div></body></html>';

// Парсинг HTML
var doc = gumbo.parse(html);

// Получение корневого узла
var root = doc.root;

// Поиск узла по идентификатору
var mainNode = gumbo.findById(root, 'main');
console.log('Main node:', mainNode);

// Получение текстового содержимого
var text = gumbo.nodeTextContent(mainNode);
console.log('Text:', text);

// Поиск узлов по классу
var contentNodes = gumbo.findByClassName(root, 'content');
console.log('Content nodes:', contentNodes);
