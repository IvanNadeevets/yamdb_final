![example workflow](https://github.com/IvanNadeevets/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# yamdb_final
* yamdb_final - это финальный проект 19 спринта курсов яндекс практикум, в котором я настроил CI/CD с помощью Github workflow.
* ip-адрес проекта 84.252.142.143:8000

## Запуск проекта
* запускаем контейнера с приложением, БД postgresql, nginx 
* запускаем миграции 
* собираем статитку 

`
docker-compose up -d --build && \
docker-compose exec web python manage.py migrate --no-input && \
docker-compose exec web python manage.py collectstatic --no-input
`

## Заведение супер пользователя
* Далее нужно завести супер-пользователя 

`docker-compose exec web bash -c \
DJANGO_SUPERUSER_USERNAME=<your_username> \
DJANGO_SUPERUSER_PASSWORD=<your_password \
DJANGO_SUPERUSER_EMAIL=<your_email> \
python manage.py createsuperuser --noinput`

* Супер-пользователь может создавать контент для базы данных через панель админа: `<адрес виртуального сервера>/admin`

## Запуск автотестов
* В корневой папке проекта запустите `pytest`

### Стек технологий используемый в проекте
* [Python: 3.8.5](https://www.python.org/)
* [Django: 3.0.5](https://www.djangoproject.com/)
* [PostgreSQL: 12.4](https://www.postgresql.org/)
* [Docker: 3.1.0](https://www.docker.com/)
* [nginx:1.19.6](https://nginx.org/)

### Лицензия
[MIT](https://choosealicense.com/licenses/mit/)

### Об авторе
* студент 10 когорты факультета Backend-разработка Яндекс Практикума
