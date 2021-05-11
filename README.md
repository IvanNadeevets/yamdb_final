![example workflow](https://github.com/IvanNadeevets/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# yamdb_final
* yamdb_final - это финальный проект 19 спринта курса "Python-разработчик Яндекс Практикум, в котором я настроил CI/CD с помощью docker-compose Github workflow.
* ip-адрес проекта 84.252.142.143


## Функциональность - Проект имитирует api для работы с социальной сетью
* Создание и авторизация пользователя с получением кода подтверждения через почту;
* Просмотр и редактирование профилей пользователей;
* Создание, просмотр, редактирование публикаций;
* Создание, просмотр, редактирование отзывов к публикациям;
* Выставление и подсчёт рейтинга для публикаций;
* Система администрирования и модерирования публикаций;
* Система поиска произведений по различным полям;

## Документация 
* Документацию для api можно найти по адресу: `<адрес виртуального сервера>\redoc`

## Запуск проекта
* запускаем контейнера с приложением, БД postgresql, nginx 
* запускаем миграции 
* собираем статитку 

`
docker-compose up -d --build && \
docker exec <web> python manage.py makemigrations --no-input && \
docker exec <web> python manage.py migrate --no-input && \
docker exec <web> python manage.py collectstatic --no-input
`

## Заведение супер пользователя
* Далее нужно завести супер-пользователя 

`docker exec -it <web> bash -c \
DJANGO_SUPERUSER_USERNAME=<your_username> \
DJANGO_SUPERUSER_PASSWORD=<your_password \
DJANGO_SUPERUSER_EMAIL=<your_email> \
python manage.py createsuperuser --noinput`

* Супер-пользователь может создавать контент для базы данных через панель админа: `<адрес виртуального сервера>/admin`

## Работа с авторизацией
* В проекте используется [Signature JWT](https://jwt.io/introduction/)
* Авторзация работает через e-mail в 3 шага:
1. сначала делаете `POST` запрос на `/api/v1/auth/mail/` с полем `email`:
```
curl --location --request POST '<адрес сервера>/api/v1/auth/mail/' \
--form 'email=example@email.com'
```
2. Оно создает в папке sent_emails файл, который будет содержать код активации 
3. Делаете `POST` запрос на `/api/v1/auth/token/` с полями `email` и `confirmation_code` и в ответ получаете токен
```
curl --location --request POST '<адрес сервера>/api/v1/auth/token/' \
--form 'email=example@email.com' \
--form 'confirmation_code=5l5-1095457590921979885c'
```
* email и прочую релеватную информацию в отсуствие доступа до api можно посмотреть в админке: '<адрес сервера>/admin'

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
