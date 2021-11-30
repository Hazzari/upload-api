# Django micro service "Image Loader"

___

Простой проект примера того как можно сделать 
API для загрузки файлов на сервер в количестве более одного

С ограничениями по размеру и формату файлов.

Демо проекта развернуто на 
[AWS-demo-api](http://18.221.147.170/api/v1/swagger/)
[AWS-front-api](http://18.117.110.164)

Для запуска проекта нужно добавить файл .env.prod в корень проекта.

Пример файла:
```shell
# .env.prod
PROJECT_NAME="image_uploader"
DEBUG=off
SECRET_KEY="django-insecure-*ah4lbk8c_44)b494it04*in2id@x$0&1vn3%*ry4v8+*1e97&0"

# добавляем хосты без пробела и скобочек
ALLOWED_HOSTS=* 

# Database
POSTGRES_DRIVER="django.db.backends.postgresql_psycopg2"
POSTGRES_DB="image_uploader"
POSTGRES_USER="image_uploader_user"
POSTGRES_PASSWORD="password"
POSTGRES_HOST=db
POSTGRES_PORT=5432

# Для entrypoint.sh
DATABASE=postgres
RUN_MIGRATE=false
```

А так же добавить файл .env.prod.db:
Пример файла:
```shell
#.env.prod.db
POSTGRES_DB="image_uploader"
POSTGRES_USER="image_uploader_user"
POSTGRES_PASSWORD="password"

PGADMIN_DEFAULT_EMAIL=admin@example.com
PGADMIN_DEFAULT_PASSWORD=admin
```

запуск докера:

```shell
#Запуск
docker-compose -f docker-compose.prod.yml up -d --build
#Миграции
docker-compose -f docker-compose.prod.yml exec web python manage.py migrate
#Статика
docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic
#Суперпользователь
docker-compose -f docker-compose.prod.yml exec web python manage.py createsuperuser
```

Адрес сервиса списка доступных API:
[LIST API](http://127.0.0.1/api/v1/swagger/)

[Регистрация](http://127.0.0.1/api/v1/user/)
[Запрос токена](http://127.0.0.1/api/v1/token/both/)
[Обновление токена](http://127.0.0.1/api/v1/token/access/)


[Загрузка файлов](http://127.0.0.1/api/v1/upload/)
Только для зарегистрированных, заголовок: 
{'Authorization: Bearer <Token>'}
