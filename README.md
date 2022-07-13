Клонировать репозиторий
git clone https://github.com/Vinsya87/yamdb_final.git
![example workflow](https://github.com/Vinsya87/yamdb_finalactions/workflows/yamdb_workflow.yml/badge.svg)


live address #######################
http://vinsteam.ddns.net/admin/
http://vinsteam.ddns.net/api/v1/
http://vinsteam.ddns.net/redoc/
-----or-----
http://51.250.100.40/admin/
http://51.250.100.40/api/v1/
http://51.250.100.40/redoc/


###############################
-Add .env file in folder infra:

```DB_ENGINE=django.db.backends.postgresql # use postgresql```

```DB_NAME=postgres # name of Database```

```POSTGRES_USER=postgres # login for Database```

```POSTGRES_PASSWORD=postgres # password for Database (create your)```

```DB_HOST=db # name of service (container)```

```DB_PORT=5432 # port to connect Database```

```SECRET_KEY=your secret cey```

-In folder infra use command:
```sudo docker-compose up -d --build```

-Make migrations:
```sudo docker-compose exec web python manage.py migrate```

-Create Superuser:
```sudo docker-compose exec web python manage.py createsuperuser```

-Collect static:
```sudo docker-compose exec web python manage.py collectstatic --no-input ```

-Open project and add test info:
```http://localhost/admin/```

-Stop project:
```sudo docker-compose down -v```

В проекте доступны следующие эндпоинты:
http://127.0.0.1:8000/api/v1/auth/signup/  - Получение кода подверждения на email

{
"email": "string",
"username": "string"
}

http://127.0.0.1:8000/api/v1/auth/token/ - Получение токена для авторизации

{
"username": "string",
"confirmation_code": "string"
}

http://127.0.0.1:8000/api/v1/categories/ - Работа с категориями, доступны запросы Get, Post и Del

http://127.0.0.1:8000/api/v1/genres/ - Работа с жанрами, доступны запросы Get, Post и Del

http://127.0.0.1:8000/api/v1/titles/ - Работа со статьями , доступны запросы Get, Post, Patch и Del

http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/  - Работа с отзывами , доступны запросы Get, Post, Patch и Del

http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/ - Работа с комментариями , доступны запросы Get, Post, Patch и Del

http://127.0.0.1:8000/api/v1/users/ - Создание пользователя и получение информации о всех пользователях. Доступны запросы Get, Post

http://127.0.0.1:8000/api/v1/users/{username}/ - Получение информации о конкретном пользователе и редактирование информации о нем. Доступны доступны запросы Get, Postm Del

http://127.0.0.1:8000/api/v1/users/me/ - Получение и изменение своих данных, доступны запросы Get, Patch

Клонирование базы

прейти в Python Shell командой

python manage.py shell

импорт необходимых модулей

import os
inport csv

установить путь до базы

path = "с:/../api_yamdb/static/data"

Сделать импорт модели:
from reviews.models import Genre, Category, Title, Review, Comment, GenreTitle
from users.models import User

Последовательно для каждой модели запустить цикл записи данных:

на примере модели пользователей.

with open('users.csv') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        p = User(id=row['id'], username=row['username'], email=row['email'], role=row['role'], bio=row['bio'], first_name=row['first_name'], last_name=row['last_name'])
        p.save()

полный набор команд в файле import_db