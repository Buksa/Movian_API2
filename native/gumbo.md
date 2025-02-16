# Документация модуля `gumbo`

Модуль `gumbo` предоставляет функции для работы с HTML-документами с использованием библиотеки Gumbo Parser. Он позволяет парсить HTML, извлекать узлы, атрибуты и текст, а также искать элементы по тегам, классам и идентификаторам. Ниже приведено подробное описание каждой функции и примеры их использования.

---

## Функции

### 1. `parse(html)`
Парсит HTML-документ и возвращает объект с корневым узлом и документом.

- **Аргументы**:
  - `html` (строка): HTML-документ для парсинга.
- **Возвращает**: Объект с двумя свойствами:
  - `document`: Корневой узел документа.
  - `root`: Корневой элемент HTML.
- **Пример**:
  ```javascript
  var html = "<html><body><div id='content'>Hello</div></body></html>";
  var result = gumbo.parse(html);
  var root = result.root;
  ```

---

### 2. `nodeType(node)`
Возвращает тип узла.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
- **Возвращает**: Число, представляющее тип узла:
  - `1`: Элемент (например, `<div>`).
  - `3`: Текстовый узел.
  - `8`: Комментарий.
  - `9`: Документ.
- **Пример**:
  ```javascript
  var type = gumbo.nodeType(node);
  console.log('Тип узла:', type);
  ```

---

### 3. `nodeName(node)`
Возвращает имя узла.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
- **Возвращает**:
  - Для элементов: Имя тега (например, `div`).
  - Для текстовых узлов: Текст.
  - Для документов: Имя документа.
- **Пример**:
  ```javascript
  var name = gumbo.nodeName(node);
  console.log('Имя узла:', name);
  ```

---

### 4. `nodeChilds(node, all)`
Возвращает дочерние узлы.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
  - `all` (булево): Если `true`, возвращает все дочерние узлы, включая текстовые и комментарии. Если `false`, возвращает только элементы.
- **Возвращает**: Массив дочерних узлов.
- **Пример**:
  ```javascript
  var childs = gumbo.nodeChilds(node, true);
  console.log('Дочерние узлы:', childs);
  ```

---

### 5. `nodeAttributes(node)`
Возвращает атрибуты узла.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
- **Возвращает**: Массив объектов, где каждый объект содержит:
  - `name`: Имя атрибута.
  - `value`: Значение атрибута.
- **Пример**:
  ```javascript
  var attributes = gumbo.nodeAttributes(node);
  console.log('Атрибуты:', attributes);
  ```

---

### 6. `nodeTextContent(node)`
Возвращает текстовое содержимое узла и его дочерних элементов.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
- **Возвращает**: Текстовое содержимое.
- **Пример**:
  ```javascript
  var text = gumbo.nodeTextContent(node);
  console.log('Текстовое содержимое:', text);
  ```

---

### 7. `findById(node, id)`
Ищет элемент по идентификатору.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
  - `id` (строка): Идентификатор элемента.
- **Возвращает**: Узел с указанным идентификатором или `null`, если не найден.
- **Пример**:
  ```javascript
  var element = gumbo.findById(node, 'content');
  console.log('Найденный элемент:', element);
  ```

---

### 8. `findByTagName(node, tagName)`
Ищет элементы по имени тега.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
  - `tagName` (строка): Имя тега (например, `div`).
- **Возвращает**: Массив элементов с указанным тегом.
- **Пример**:
  ```javascript
  var elements = gumbo.findByTagName(node, 'div');
  console.log('Найденные элементы:', elements);
  ```

---

### 9. `findByClassName(node, className)`
Ищет элементы по классу.

- **Аргументы**:
  - `node` (объект): Узел, полученный из `parse`.
  - `className` (строка): Имя класса (например, `my-class`).
- **Возвращает**: Массив элементов с указанным классом.
- **Пример**:
  ```javascript
  var elements = gumbo.findByClassName(node, 'my-class');
  console.log('Найденные элементы:', elements);
  ```

---

## Пример использования

Пример использования модуля `gumbo` в среде JavaScript (ES5.1):

```javascript
var gumbo = require('native/gumbo');

// Парсинг HTML
var html = "<html><body><div id='content' class='my-class'>Hello</div></body></html>";
var result = gumbo.parse(html);
var root = result.root;

// Получение типа узла
var type = gumbo.nodeType(root);
console.log('Тип корневого узла:', type);

// Получение имени узла
var name = gumbo.nodeName(root);
console.log('Имя корневого узла:', name);

// Поиск элемента по ID
var element = gumbo.findById(root, 'content');
if (element) {
  console.log('Найденный элемент:', element);
}

// Поиск элементов по классу
var elements = gumbo.findByClassName(root, 'my-class');
console.log('Найденные элементы:', elements);

// Получение текстового содержимого
var text = gumbo.nodeTextContent(element);
console.log('Текстовое содержимое:', text);
```

---

## Примечания

- Модуль `gumbo` использует библиотеку Gumbo Parser для парсинга HTML, что обеспечивает высокую производительность и точность.
- Все функции работают с узлами, которые возвращаются после парсинга HTML.
- Убедитесь, что HTML-документ корректен, чтобы избежать ошибок при парсинге.

Этот модуль предоставляет мощный набор функций для работы с HTML-документами, что делает его подходящим для задач, таких как извлечение данных, анализ структуры и манипуляции с DOM.
