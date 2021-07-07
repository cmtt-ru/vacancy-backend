# Тестовое задание

Необходимо разработать небольшой API для создания и открутки рекламных объявлений без использования фреймворков — подключите необходимые библиотеки через Composer. Для хранения объявлений можете использовать любое хранилище.

API состоит из трёх роутов: создания, редактирования и открутки

### Создание объявления

Пример запроса

```http request
POST /ads HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded
...

text=Advertisement1&price=300&limit=1000&banner=https://linktoimage.png
```

Описание полей

| Поле | Описание  | Тип  |
|---|---|---|
| text | Заголовок объявления | Строковый |
| price | Стоимость одного показа | Числовой |
| limit | Лимит показов | Числовой |
| banner | Ссылка на картинку | Строковый |


Пример ответа

```http request
HTTP/1.1 200 OK
Content-Type: application/json
...

{
  "message": "OK",
  "code": 200,
  "data": {
     "id": 123,
     "text": "Advertisement1",
     "banner": "https://linktoimage.png"   
  }
}
```

Пример ответа с ошибкой валидации поля

```http request
HTTP/1.1 200 OK
Content-Type: application/json
...

{
  "message": "Invalid banner link",
  "code": 400,
  "data": {}
}
```

### Открутка объявления

Возвращается _id_, _text_ и _banner_ объявления. Выбирается по следующим условиям:

- У него должно быть самая высокая цена. _Приветствуется использование более хитрого алгоритма_
- Количество открученных показов этого объявления не должно превышать лимит
  показов (поле limit).

Пример запроса

```http request
GET /ads/relevant HTTP/1.1
Host: localhost
...
```

Пример ответа

```http request
HTTP/1.1 200 OK
Content-Type: application/json
...

{
  "message": "OK",
  "code": 200,
  "data": {
     "id": 123,
     "text": "Advertisement1",
     "banner": "https://linktoimage.png"   
  }
}
```

### Редактирование объявление

Пример запроса

```http request
POST /ads/1234 HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded
...

text=Advertisement123&price=450&limit=1200&banner=https://linktoimage.png
```

Пример ответа

```http request
HTTP/1.1 200 OK
Content-Type: application/json
...

{
  "message": "OK",
  "code": 200,
  "data": {
    "id": 123,
    "text": "Advertisement123",
    "banner": "https://linktoimage.png"
  }
}
```

## Требования к тестовому заданию

- Мы хотим видеть ООП-подход и как можно более аккуратный и красивый архитектурно код на PHP 7 и PSR-12
- Документирование кода: описание методов и инструкция по разворачиванию проекта
- Результат в виде github-репозитория
- Docker-контейнеры для тестирования

## Бонусные пункты

- Использование статических анализаторов
- Покрытие кода юнит-тестами.