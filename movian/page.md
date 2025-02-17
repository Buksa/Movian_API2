Вот обновленная документация с более подробными примерами для модуля `movian/prop` и `movian/settings`:

---

# Документация модуля `movian/page`

Этот модуль предоставляет функциональность для работы с объектами страниц и элементов в Movian. Он позволяет создавать страницы, добавлять элементы, управлять метаданными и обрабатывать события.

---

## Содержание
1. [Класс `Item`](#класс-item)
   - [Создание элемента](#создание-элемента)
   - [Методы](#методы-item)
2. [Класс `Page`](#класс-page)
   - [Создание страницы](#создание-страницы)
   - [Методы](#методы-page)
3. [Экспортируемые функции](#экспортируемые-функции)
   - [`Route`](#route)
   - [`Searcher`](#searcher)

---

## Класс `Item`

Класс `Item` представляет элемент на странице. Элемент может быть видео, действием, разделителем и т.д.

### Создание элемента
```javascript
var item = new Item(page);
```
- `page` — Объект страницы, к которой принадлежит элемент.

### Методы `Item`

#### `bindVideoMetadata(obj)`
Привязывает метаданные видео к элементу.

**Параметры:**
- `obj` — Объект метаданных.

**Пример:**
```javascript
item.bindVideoMetadata({
    title: "My Video",
    duration: 120,
    description: "This is a sample video.",
    poster: "http://example.com/poster.jpg"
});
```

#### `unbindVideoMetadata()`
Отвязывает метаданные видео от элемента.

**Пример:**
```javascript
item.unbindVideoMetadata();
```

#### `toString()`
Возвращает строковое представление элемента.

**Пример:**
```javascript
console.log(item.toString()); // [ITEM with title: My Video]
```

#### `dump()`
Выводит информацию о элементе в консоль.

**Пример:**
```javascript
item.dump();
```

#### `enable()`
Включает элемент.

**Пример:**
```javascript
item.enable();
```

#### `disable()`
Отключает элемент.

**Пример:**
```javascript
item.disable();
```

#### `destroyOption(item)`
Уничтожает опцию элемента.

**Пример:**
```javascript
item.destroyOption(optionItem);
```

#### `addOptAction(title, func, subtype)`
Добавляет действие в опции элемента.

**Параметры:**
- `title` — Заголовок действия.
- `func` — Функция, вызываемая при активации действия.
- `subtype` — Подтип действия.

**Пример:**
```javascript
item.addOptAction("Play", function() {
    console.log("Play clicked!");
}, "play");
```

#### `addOptURL(title, url, subtype)`
Добавляет URL в опции элемента.

**Параметры:**
- `title` — Заголовок URL.
- `url` — URL.
- `subtype` — Подтип URL.

**Пример:**
```javascript
item.addOptURL("Open Link", "http://example.com", "link");
```

#### `addOptSeparator(title)`
Добавляет разделитель в опции элемента.

**Параметры:**
- `title` — Заголовок разделителя.

**Пример:**
```javascript
item.addOptSeparator("Section 1");
```

#### `destroy()`
Уничтожает элемент.

**Пример:**
```javascript
item.destroy();
```

#### `moveBefore(before)`
Перемещает элемент перед указанным элементом.

**Параметры:**
- `before` — Элемент, перед которым нужно переместить текущий элемент.

**Пример:**
```javascript
item.moveBefore(otherItem);
```

#### `onEvent(type, callback)`
Регистрирует обработчик события.

**Параметры:**
- `type` — Тип события.
- `callback` — Функция-обработчик.

**Пример:**
```javascript
item.onEvent("click", function() {
    console.log("Item clicked!");
});
```

---

## Класс `Page`

Класс `Page` представляет страницу, содержащую элементы.

### Создание страницы
```javascript
var page = new Page(root, sync, flat);
```
- `root` — Корневой объект страницы.
- `sync` — Флаг синхронности.
- `flat` — Флаг плоской структуры.

### Методы `Page`

#### `haveMore(v)`
Указывает, есть ли еще элементы для загрузки.

**Параметры:**
- `v` — Логическое значение.

**Пример:**
```javascript
page.haveMore(true);
```

#### `findItemByProp(v)`
Находит элемент по свойству.

**Параметры:**
- `v` — Свойство элемента.

**Пример:**
```javascript
var index = page.findItemByProp(prop);
```

#### `error(msg)`
Устанавливает сообщение об ошибке на странице.

**Параметры:**
- `msg` — Сообщение об ошибке.

**Пример:**
```javascript
page.error("Failed to load data");
```

#### `getItems()`
Возвращает список элементов на странице.

**Пример:**
```javascript
var items = page.getItems();
```

#### `appendItem(url, type, metadata)`
Добавляет элемент на страницу.

**Параметры:**
- `url` — URL элемента.
- `type` — Тип элемента.
- `metadata` — Метаданные элемента.

**Пример:**
```javascript
var item = page.appendItem("http://example.com/video.mp4", "video", {
    title: "My Video",
    duration: 120,
    description: "This is a sample video.",
    poster: "http://example.com/poster.jpg"
});
```

#### `appendAction(title, func, subtype)`
Добавляет действие на страницу.

**Параметры:**
- `title` — Заголовок действия.
- `func` — Функция, вызываемая при активации действия.
- `subtype` — Подтип действия.

**Пример:**
```javascript
page.appendAction("Play", function() {
    console.log("Play clicked!");
}, "play");
```

#### `appendPassiveItem(type, data, metadata)`
Добавляет пассивный элемент на страницу.

**Параметры:**
- `type` — Тип элемента.
- `data` — Данные элемента.
- `metadata` — Метаданные элемента.

**Пример:**
```javascript
page.appendPassiveItem("text", "Hello, World!", {
    title: "Message",
    description: "This is a sample message."
});
```

#### `dump()`
Выводит информацию о странице в консоль.

**Пример:**
```javascript
page.dump();
```

#### `flush()`
Очищает страницу от всех элементов.

**Пример:**
```javascript
page.flush();
```

#### `redirect(url)`
Перенаправляет страницу на указанный URL.

**Параметры:**
- `url` — URL для перенаправления.

**Пример:**
```javascript
page.redirect("http://example.com/new-page");
```

#### `onEvent(type, callback)`
Регистрирует обработчик события.

**Параметры:**
- `type` — Тип события.
- `callback` — Функция-обработчик.

**Пример:**
```javascript
page.onEvent("load", function() {
    console.log("Page loaded!");
});
```

---

## Экспортируемые функции

### `Route`

Создает маршрут для обработки запросов.

**Пример:**
```javascript
var route = new exports.Route(/^myplugin\/(.*)$/, function(page, arg1) {
    console.log("Route matched with arg:", arg1);
    page.appendItem("http://example.com/video.mp4", "video", {
        title: "My Video",
        duration: 120
    });
});
```

#### `destroy()`
Уничтожает маршрут.

**Пример:**
```javascript
route.destroy();
```

### `Searcher`

Создает поисковый хук.

**Пример:**
```javascript
var searcher = new exports.Searcher("My Search", "search-icon", function(page, query) {
    console.log("Search query:", query);
    page.appendItem("http://example.com/video.mp4", "video", {
        title: "Search Result",
        description: "This is a search result for: " + query
    });
});
```

#### `destroy()`
Уничтожает поисковый хук.

**Пример:**
```javascript
searcher.destroy();
```

---

Этот модуль предоставляет мощные инструменты для создания и управления страницами и элементами в Movian, что делает его полезным для разработки плагинов и расширений.
