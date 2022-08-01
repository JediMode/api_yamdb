# Проект YaMDb
 Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка». 
 В каждой категории есть произведения: книги, фильмы или музыка. 
 Произведению может быть присвоен жанр. Новые жанры может создавать только администратор.
 Пользователи могут оставить к произведениям текстовые отзывы и поставить произведению оценку (в диапазоне от одного до десяти).
 Из пользовательских оценок формируется усреднённая оценка произведения — рейтинг.
 
 Аутентификация по JWT-токену.
 Поддерживает методы GET, POST, PUT, PATCH, DELETE.
 Предоставляет данные в формате JSON.
 Создан в команде из трех человек с использованием Git в рамках учебного курса Яндекс.Практикум.
 
# Стек технологий
- проект написан на Python с использованием веб-фреймворка Django REST Framework
- библиотека Simple JWT - работа с JWT-токеном
- библиотека django-filter - фильтрация запросов
- база данных - SQLite
- система управления версиями - git

# Как запустить проект:
Клонировать репозиторий и перейти в него в командной строке:
```
    cd api_yamdb
```
Cоздать и активировать виртуальное окружение:
```
    python3 -m venv env
```
```
    source env/bin/activate
```
Установить зависимости из файла requirements.txt:
```
    python3 -m pip install --upgrade pip
```
```
    pip install -r requirements.txt
```
Выполнить миграции:
```
    python3 manage.py migrate
```
Создайте суперпользователя:
```
    python3 manage.py createsuperuser
```
Запустить проект:
```
    python3 manage.py runserver
```
____
Ваш проект запустился на http://127.0.0.1:8000/  
Полная документация (redoc.yaml) доступна по адресу http://127.0.0.1:8000/redoc/  
C помощью команды pytest вы можете запустить тесты и проверить работу модулей 

# Алгоритм регистрации новых пользователей

1. Пользователь отправляет POST-запрос с параметрами email и username на эндпоинт /api/v1/auth/signup/.
2. Сервис YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на указанный адрес email.
3. Пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).

В результате пользователь получает токен и может работать с API проекта, отправляя этот токен с каждым запросом.
После регистрации и получения токена пользователь может отправить PATCH-запрос на эндпоинт /api/v1/users/me/ и заполнить поля в своём профайле (описание полей — в документации).

## Ресурсы API YaMDb
- Ресурс auth: аутентификация.
- Ресурс users: пользователи.
- Ресурс titles: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).
- Ресурс categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»).
- Ресурс genres: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
- Ресурс reviews: отзывы на произведения. Отзыв привязан к определённому произведению.
- Ресурс comments: комментарии к отзывам. Комментарий привязан к определённому отзыву.

## Пример http-запроса (POST) 
```
    url = 'http://127.0.0.1:8000/api/v1/titles/  
    data = {"name": "string", "year": 0, "description": "string", "genre": ["string"], "category": "string"}  
    headers = {'Authorization': 'Bearer your_token'}  
    request = request.post(url, data=data, headers=headers)  
```
## Ответ API_YaMDb:
```
Статус - код 200
{
"id": 0,
"name": "string",
"year": 0,
"rating": 0,
"description": "string",
"genre": [
{}
],
"category": {
"name": "string",
"slug": "string"
}
}
```
