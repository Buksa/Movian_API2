# Metadata Module Functions

Модуль `metadata` предоставляет функции для работы с метаданными. Ниже приведены подробные описания и примеры для каждой функции.

---

## Основные функции

### 1. **`metadata.videoMetadataBind(prop, url, options)`**

- **Описание**: Связывает метаданные видео с указанным свойством.
- **Параметры**:
  - `prop` (`Object`): Свойство для связывания
  - `url` (`string`): URL видео
  - `options` (`Object`): Опции метаданных:
    - `filename` (`string`): Имя файла (опционально)
    - `title` (`string`): Название видео (опционально)
    - `year` (`number`): Год выпуска (опционально)
    - `season` (`number`): Сезон (опционально)
    - `episode` (`number`): Эпизод (опционально)
    - `imdb` (`string`): IMDB ID (опционально)
    - `duration` (`number`): Длительность в секундах (опционально)
- **Возвращаемое значение**: `Object` - Объект метаданных
- **Пример**:
    ```js
    var prop = {};
    var metadata = metadata.videoMetadataBind(prop, 'https://example.com/video.mp4', {
      title: 'My Video',
      year: 2023,
      duration: 120
    });
    ```

### 2. **`metadata.bindPlayInfo(prop, url)`**

- **Описание**: Связывает информацию о воспроизведении с указанным свойством.
- **Параметры**:
  - `prop` (`Object`): Свойство для связывания
  - `url` (`string`): URL видео
- **Пример**:
    ```js
    var prop = {};
    metadata.bindPlayInfo(prop, 'https://example.com/video.mp4');
    ```

## Пример использования модуля в среде JavaScript (ES5.1)

```js
// Пример использования модуля metadata
var prop = {};

// Связывание метаданных видео
var videoMetadata = metadata.videoMetadataBind(prop, 'https://example.com/video.mp4', {
  title: 'My Video',
  year: 2023,
  duration: 120
});

// Связывание информации о воспроизведении
metadata.bindPlayInfo(prop, 'https://example.com/video.mp4');

// Использование связанных данных
console.log('Video Metadata:', videoMetadata);
console.log('Play Info:', prop);
