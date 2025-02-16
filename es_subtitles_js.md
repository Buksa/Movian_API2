# Subtitle Module Functions

Модуль `subtitle` предоставляет функции для работы с субтитрами, включая добавление провайдеров субтитров и элементов субтитров. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`subtitle.addProvider(id, title, callback)`**

- **Описание**: Добавляет провайдера субтитров.
- **Параметры**:
  - `id` (`string`): Идентификатор провайдера
  - `title` (`string`): Название провайдера
  - `callback` (`function`): Функция обратного вызова для обработки запросов
- **Возвращаемое значение**: `Object` - Объект провайдера субтитров
- **Пример**:
    ```js
    subtitle.addProvider('myProvider', 'My Provider', function(prop, query, score, autosel) {
      console.log('Query:', query);
    });
    ```

### 2. **`subtitle.addItem(prop, url, title, language, format, source, score, autosel)`**

- **Описание**: Добавляет элемент субтитров.
- **Параметры**:
  - `prop` (`Object`): Объект свойства
  - `url` (`string`): URL субтитров
  - `title` (`string`): Название субтитров
  - `language` (`string`): Язык субтитров
  - `format` (`string`): Формат субтитров
  - `source` (`string`): Источник субтитров
  - `score` (`number`): Оценка субтитров
  - `autosel` (`boolean`): Автоматически выбирать субтитры
- **Пример**:
    ```js
    subtitle.addItem(myProp, 'https://example.com/subtitles.srt', 'Subtitles', 'en', 'srt', 'example.com', 100, true);
    ```

### 3. **`subtitle.getLanguages()`**

- **Описание**: Возвращает массив поддерживаемых языков субтитров.
- **Возвращаемое значение**: `Array` - Массив языков
- **Пример**:
    ```js
    var languages = subtitle.getLanguages();
    console.log('Languages:', languages);
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля subtitle

// Добавление провайдера субтитров
var provider = subtitle.addProvider('myProvider', 'My Provider', function(prop, query, score, autosel) {
  console.log('Query:', query);
});

// Добавление элемента субтитров
subtitle.addItem(myProp, 'https://example.com/subtitles.srt', 'Subtitles', 'en', 'srt', 'example.com', 100, true);

// Получение поддерживаемых языков
var languages = subtitle.getLanguages();
console.log('Languages:', languages);
