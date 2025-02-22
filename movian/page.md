---

# Документация класса `Page`

Класс `Page` представляет страницу, которая может содержать элементы, такие как видео, действия, разделители и другие. Он используется для создания и управления содержимым страницы в Movian.

---

## Создание страницы

```javascript
var page = new Page(root, sync, flat);
```
- `root` — Корневой объект страницы.
- `sync` — Флаг синхронности (если `true`, страница будет обрабатываться синхронно).
- `flat` — Флаг плоской структуры (если `true`, страница будет иметь плоскую структуру).

**Пример:**
```javascript
var root = prop.createRoot("myPage");
var page = new Page(root, false, false);
```

---

## Методы класса `Page`

### `appendItem(url, type, metadata)`
Добавляет элемент на страницу.

**Параметры:**
- `url` — URL элемента.
- `type` — Тип элемента (например, `"video"`, `"directory"`).
- `metadata` — Объект метаданных для элемента.

**Пример:**
```javascript
var item = page.appendItem("http://example.com/video.mp4", "video", {
    title: "My Video",
    duration: 120,
    description: "This is a sample video.",
    poster: "http://example.com/poster.jpg"
});
```

### `appendAction(title, func, subtype)`
Добавляет действие на страницу.

**Параметры:**
- `title` — Заголовок действия.
- `func` — Функция, вызываемая при активации действия.
- `subtype` — Подтип действия (например, `"play"`).

**Пример:**
```javascript
page.appendAction("Play", function() {
    console.log("Play clicked!");
}, "play");
```

### `appendPassiveItem(type, data, metadata)`
Добавляет пассивный элемент на страницу.

**Параметры:**
- `type` — Тип элемента (например, `"text"`).
- `data` — Данные элемента.
- `metadata` — Метаданные элемента.

**Пример:**
```javascript
page.appendPassiveItem("text", "Hello, World!", {
    title: "Message",
    description: "This is a sample message."
});
```

### `redirect(url)`
Перенаправляет страницу на указанный URL.

**Параметры:**
- `url` — URL для перенаправления.

**Пример:**
```javascript
page.redirect("http://example.com/new-page");
```

### `onEvent(type, callback)`
Регистрирует обработчик события.

**Параметры:**
- `type` — Тип события (например, `"load"`).
- `callback` — Функция, вызываемая при срабатывании события.

**Пример:**
```javascript
page.onEvent("load", function() {
    console.log("Page loaded!");
});
```

---

## Метод `bindVideoMetadata`

Метод `bindVideoMetadata` привязывает метаданные видео к элементу. Он используется для управления метаданными, такими как название, продолжительность, описание и постер.

### Использование
```javascript
item.bindVideoMetadata(metadata);
```
- `metadata` — Объект метаданных, который должен содержать следующие поля:
  - `title` — Название видео.
  - `duration` — Продолжительность видео в секундах.
  - `description` — Описание видео.
  - `poster` — URL постера видео.
  - `year` — Год выпуска видео (опционально).
  - `season` — Сезон (опционально).
  - `episode` — Эпизод (опционально).
  - `imdb` — IMDb ID (опционально).

**Пример:**
```javascript
item.bindVideoMetadata({
    title: "My Video",
    duration: 120,
    description: "This is a sample video.",
    poster: "http://example.com/poster.jpg",
    year: 2020,
    season: 1,
    episode: 2,
    imdb: "tt1234567"
});
```

### Проверка входящего объекта
В коде видно, что метод `bindVideoMetadata` ожидает объект с полями:
- `title` — Название видео.
- `duration` — Продолжительность видео.
- `description` — Описание видео.
- `poster` — URL постера.
- `year` — Год выпуска.
- `season` — Сезон.
- `episode` — Эпизод.
- `imdb` — IMDb ID.

Если какие-то поля отсутствуют, они будут проигнорированы.

---

## Пример использования класса `Page`

```javascript
var prop = require('movian/prop');
var root = prop.createRoot("myPage");
var page = new Page(root, false, false);

// Добавляем видео
var videoItem = page.appendItem("http://example.com/video.mp4", "video", {
    title: "My Video",
    duration: 120,
    description: "This is a sample video.",
    poster: "http://example.com/poster.jpg"
});

// Привязываем метаданные
videoItem.bindVideoMetadata({
    title: "My Video",
    duration: 120,
    description: "This is a sample video.",
    poster: "http://example.com/poster.jpg",
    year: 2020,
    season: 1,
    episode: 2,
    imdb: "tt1234567"
});

// Добавляем действие
page.appendAction("Play", function() {
    console.log("Play clicked!");
}, "play");

// Регистрируем обработчик события
page.onEvent("load", function() {
    console.log("Page loaded!");
});
```

---
