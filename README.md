## Описание проекта:

* Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором.
* В каждой категории есть произведения: книги, фильмы или музыка. 
* Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.
* Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения (рейтинг). На одно произведение пользователь может оставить только один отзыв.

Полный список возможных запросов и соответствующих ответов можно найти в документации по следующей ссылке:

[http://127.0.0.1/redoc/](http://127.0.0.1/redoc/)

### Ссылка заработает только после запуска проекта, о чем речь пойдет ниже.

## Как запустить проект:

Клонируйте репозиторий и перейдите в него в командной строке: 
 
``` bash
git clone https://github.com/DanteMoren/infra_sp2.git
``` 
 
``` bash
cd infra_sp
``` 
 
Cоздайте файл .env и внесите в него следующие данные: 
 
``` 
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
SECRET_KEY= #введите свой ключ из settings.py
``` 
 
Выполните комманды
 
``` bash
docker-compose up -d 
docker-compose exec web python manage.py migrate --noinput
docker-compose exec web python manage.py collectstatic --no-input 
``` 
Выполните комманду для создания суперпользователя и введите логин, почту и пароль
```bash
docker-compose exec web python manage.py createsuperuser
```



## Как зарегистрироваться и получить *JWT-токен*

1. Отправьте POST-запрос с параметрами *email* и *username* на эндпоинт ```/api/v1/auth/signup/```;
2. Сервис YaMDB отправит вас письмо с кодом подтверждения (*confirmation_code*) на указанный адрес *email*;
3. Отправьте POST-запрос с параметрами *username* и *confirmation_code* на эндпоинт ```/api/v1/auth/token/```. В ответе на запрос вы получите *JWT-token*;
4. После регистрации и получения токена можете отправить PATCH-запрос на эндпоинт ```/api/v1/users/me/``` и заполнить поля в своём профайле (описание полей — в документации).

### Теперь вы можете работать с API проекта, отправляя полученный токен при каждом запросе :) ###

![example workflow](https://github.com/DanteMoren/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)