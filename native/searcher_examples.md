# Подробный пример использования модуля `searcher`

Модуль `searcher` позволяет выполнять поиск и передавать результаты в JavaScript для дальнейшей обработки. В этом примере мы рассмотрим, как можно использовать этот модуль для реализации поиска по данным, обработки результатов и обновления интерфейса пользователя.

---

## Пример: Поиск по списку видео

### 1. Подготовка данных

Предположим, у нас есть список видео, который мы хотим искать. Данные могут быть представлены в виде массива объектов:

```javascript
var videos = [
  { title: 'Introduction to JavaScript', duration: 120, url: 'https://example.com/intro-js' },
  { title: 'Advanced JavaScript Techniques', duration: 180, url: 'https://example.com/advanced-js' },
  { title: 'React for Beginners', duration: 150, url: 'https://example.com/react-beginners' },
  { title: 'Node.js Crash Course', duration: 200, url: 'https://example.com/nodejs-crash-course' }
];
```

---

### 2. Создание модели данных

Мы создадим объект свойства, который будет представлять модель данных для поиска:

```javascript
var prop = require('prop');
var model = prop.create('videoList');
```

---

### 3. Реализация поиска

Теперь реализуем функцию поиска, которая будет вызываться при вводе пользователем поискового запроса:

```javascript
var searcher = require('searcher');

function performSearch(query) {
  // Объект свойства, указывающий на состояние загрузки
  var loading = prop.create('loading');
  prop.set(loading, 'status', true); // Устанавливаем состояние загрузки

  // Выполняем поиск
  searcher.search(model, query, loading);

  // Обработка результатов поиска
  searcher.onSearch(function(model, query, loading) {
    console.log('Поисковый запрос:', query);

    // Фильтрация видео по запросу
    var results = videos.filter(function(video) {
      return video.title.toLowerCase().includes(query.toLowerCase());
    });

    // Обновление модели данных с результатами поиска
    prop.set(model, 'results', results);

    // Обновление состояния загрузки
    prop.set(loading, 'status', false);
  });
}
```

---

### 4. Обновление интерфейса пользователя

Теперь добавим логику для обновления интерфейса пользователя на основе результатов поиска:

```javascript
function updateUI() {
  // Подписка на изменения модели данных
  prop.subscribe(model, { autoDestroy: true }, function(event, value) {
    if (event === 'set' && value.results) {
      // Очистка текущего списка видео
      clearVideoList();

      // Отображение результатов поиска
      value.results.forEach(function(video) {
        addVideoToList(video);
      });
    }
  });

  // Подписка на изменения состояния загрузки
  var loading = prop.getChild(model, 'loading');
  prop.subscribe(loading, { autoDestroy: true }, function(event, value) {
    if (event === 'set' && value.status !== undefined) {
      if (value.status) {
        showLoadingIndicator();
      } else {
        hideLoadingIndicator();
      }
    }
  });
}

// Функции для работы с интерфейсом
function clearVideoList() {
  console.log('Очистка списка видео...');
}

function addVideoToList(video) {
  console.log('Добавление видео:', video.title);
}

function showLoadingIndicator() {
  console.log('Показать индикатор загрузки...');
}

function hideLoadingIndicator() {
  console.log('Скрыть индикатор загрузки...');
}
```

---

### 5. Интеграция с пользовательским интерфейсом

Теперь интегрируем поиск с пользовательским интерфейсом. Например, при вводе текста в поле поиска:

```javascript
// Эмуляция ввода пользователя
var searchInput = 'JavaScript';

// Выполнение поиска при вводе текста
performSearch(searchInput);

// Обновление интерфейса
updateUI();
```

---

### 6. Полный пример

Вот полный пример кода:

```javascript
var prop = require('prop');
var searcher = require('searcher');

// Данные
var videos = [
  { title: 'Introduction to JavaScript', duration: 120, url: 'https://example.com/intro-js' },
  { title: 'Advanced JavaScript Techniques', duration: 180, url: 'https://example.com/advanced-js' },
  { title: 'React for Beginners', duration: 150, url: 'https://example.com/react-beginners' },
  { title: 'Node.js Crash Course', duration: 200, url: 'https://example.com/nodejs-crash-course' }
];

// Модель данных
var model = prop.create('videoList');

// Функция поиска
function performSearch(query) {
  var loading = prop.create('loading');
  prop.set(loading, 'status', true);

  searcher.search(model, query, loading);

  searcher.onSearch(function(model, query, loading) {
    console.log('Поисковый запрос:', query);

    var results = videos.filter(function(video) {
      return video.title.toLowerCase().includes(query.toLowerCase());
    });

    prop.set(model, 'results', results);
    prop.set(loading, 'status', false);
  });
}

// Обновление интерфейса
function updateUI() {
  prop.subscribe(model, { autoDestroy: true }, function(event, value) {
    if (event === 'set' && value.results) {
      clearVideoList();
      value.results.forEach(function(video) {
        addVideoToList(video);
      });
    }
  });

  var loading = prop.getChild(model, 'loading');
  prop.subscribe(loading, { autoDestroy: true }, function(event, value) {
    if (event === 'set' && value.status !== undefined) {
      if (value.status) {
        showLoadingIndicator();
      } else {
        hideLoadingIndicator();
      }
    }
  });
}

// Функции для работы с интерфейсом
function clearVideoList() {
  console.log('Очистка списка видео...');
}

function addVideoToList(video) {
  console.log('Добавление видео:', video.title);
}

function showLoadingIndicator() {
  console.log('Показать индикатор загрузки...');
}

function hideLoadingIndicator() {
  console.log('Скрыть индикатор загрузки...');
}

// Эмуляция ввода пользователя
var searchInput = 'JavaScript';
performSearch(searchInput);
updateUI();
```

---

## Примечания

- В этом примере показано, как можно использовать модуль `searcher` для реализации поиска по данным и обновления интерфейса пользователя.
- Модель данных (`model`) используется для хранения результатов поиска и состояния загрузки.
- Функция `performSearch` выполняет поиск и обновляет модель данных, а функция `updateUI` обновляет интерфейс на основе изменений модели.

Этот пример демонстрирует, как можно интегрировать поиск с пользовательским интерфейсом и обрабатывать результаты в реальном времени.
