## Описание

API для Yatube представляет собой проект социальной сети в которой реализованы возможности 
публиковать записи, комментировать записи, а так же подписываться или отписываться от авторов.

## Запуск проекта в dev-режиме

- Клонировать репозиторий и перейти в него в командной строке.
- Установить и активировать виртуальное окружение версии Python 3.10:

```cmd
py -3.10 -m venv venv
```

```cmd
./venv/Scripts/activate
```

- Установить все зависимости из файла requirements.txt

```cmd
pip install -r requirements.txt
```

- Выполнить миграции:

```cmd
cd yatube_api
```

```cmd
python manage.py migrate
```

- Создать суперпользователя:

```bash
python manage.py createsuperuser
```

- Запустить проект:

```bash
python manage.py runserver
```

## Примеры работы с API для всех пользователей

Для неавторизованных пользователей работа с API доступна в режиме чтения, что-либо изменить или создать не получится.

```r
GET api/v1/posts/ - получить список всех публикаций.
При указании параметров limit и offset выдача должна работать с пагинацией
GET api/v1/posts/{id}/ - получение публикации по id
GET api/v1/groups/ - получение списка доступных сообществ
GET api/v1/groups/{id}/ - получение информации о сообществе по id
GET api/v1/{post_id}/comments/ - получение всех комментариев к публикации
GET api/v1/{post_id}/comments/{id}/ - Получение комментария к публикации по id
```

## Примеры работы с API для авторизованных пользователей

- Для создания публикации используем:

```r
POST /api/v1/posts/
```

в теле запроса:

```json
{
"text": "string",
"image": "string",
"group": 0
}
```

- Обновление публикации:

```r
PUT /api/v1/posts/{id}/
```

в теле запроса:

```json
{
"text": "string",
"image": "string",
"group": 0
}
```

- Частичное обновление публикации:

```r
PATCH /api/v1/posts/{id}/
```

в теле запроса:

```json
{
"text": "string",
"image": "string",
"group": 0
}
```

- Удаление публикации:

```r
DEL /api/v1/posts/{id}/
```
Эндпоинт /api/v1/follow/ (подписки) доступен только для авторизованных пользователей.

Подписка пользователя, от имени которого сделан запрос, на пользователя переданного в теле запроса:

```r
POST /api/v1/follow/
```

в теле запроса:

```json
{
"following": "string"
}
```

## Добавить группу в проект нужно через админ панель Django:

после авторизации, переходим в раздел Groups и создаем группы.

```r
admin/
```

- Доступ авторизованным пользователем доступен по JWT-токену, который можно получить выполнив POST запрос по адресу:

```r
POST /api/v1/jwt/create/
```

- Передав в body данные пользователя:

```json
{
"username": "string",
"password": "string"
}
```

- Полученный токен добавляем в headers, после чего буду доступны все функции проекта:

```r
Authorization: Bearer {your_token}
```

- Обновить JWT-токен:

```r
POST /api/v1/jwt/refresh/
```

- Проверить JWT-токен:

```r
POST /api/v1/jwt/verify/
```
- В запущенном проекте доступна документация по адресу:

```r
http://127.0.0.1:8000/redoc/
```
