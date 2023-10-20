#  Foodgram

## Описание проекта

Проект Foodgram реализует сервис - базу данных кулинарных рецептов. Неавторизованные посетители могут просматривать рецепты и страницы пользователей.
Зарегистрированные пользователи могут созавать собственные рецепты, подписываться на рецепты других пользователей, добавлять понравившиеся рецепты в "Избранное", а также скачивать список и количество необходимых продуктов, для приготовления выбранных (добавленых в корзину) рецептов.

## Используемые технологии

- Python
- Django
- Django REST framework
- Node.js
- Docker
- PostgreSQL
- Nginx

## Запуск приложения в Ubuntu/Debian Linux

Установка и запуск приложения на сервер возможна в двух вариантах. Из исходных кодов на Github вручную и c использованием CI/CD GitHub Actions

### Из исходных кодов GitHub

1. Создать на сервере в домашнем каталоге каталог `foodgram`:

```
$ mkdir foodgram
```

2. Клонировать репозиторий:

```bash 
$ git@github.com:SpeedeGonzales/foodgram-project-react.git
```

3. В корневом каталоге проекта из файла `.env.example` создать файл `.env`, заменив при необходимости значения переменных.

```bash 
$ cp .env.example .env
```

4. Установить на сервер Docker Compose:

```
$ sudo apt update
$ sudo apt install curl
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo apt install docker-compose-plugin
```

5. Запустить в каталоге `foodgram` Docker Compose в режиме демона:
```
$ sudo docker compose up -d
```
В результате соберутся и запустятся необходимые контейнеры.

6. Выполнить следующие команды:
```
$ sudo docker compose exec backend python manage.py migrate
$ sudo docker compose exec backend python manage.py collectstatic --noinput
sudo docker compose exec backend mv /static/rest_framework /static/static/
sudo docker compose exec backend mv /static/admin /static/static/
```

7. Создайте администратора базы данных
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser
```

8. Установить согласно документации Nginx. В конфигурационном файле `/etc/nginx/sites-enabled/default` в секции `server` изменить настройки `location`:

```
location / {
    proxy_set_header Host $http_host;
    proxy_pass http://127.0.0.1:9000;
}
```

9. Перезапустить Nginx:

```
$ sudo service nginx reload
```
После этого приложение будет доступно по IP адресу сервера либо localhost

### C использованием CI/CD GitHub Actions на удаленный сервер

1. Форкните в свой аккаунт GitHub репозиторий git@github.com:SpeedeGonzales/kittygram_final.git

2. Добавте secrets в  GitHub Actions форкутого репозитария:

```
    DOCKER_USERNAME                # имя пользователя в DockerHub
    DOCKER_PASSWORD                # пароль пользователя в DockerHub
    HOST                           # IP-адрес сервера
    USER                           # имя пользователя
    SSH_KEY                        # содержимое приватного SSH-ключа
    SSH_PASSPHRASE                 # пароль для SSH-ключа

    TELEGRAM_TO                    # ID вашего телеграм-аккаунта
    TELEGRAM_TOKEN                 # токен вашего бота
```
3. Сборка и деплой на сервер проект происходит при каждом новом коммите, после команды git push


## Адрес проекта:
https://foodgram.akbsib.ru/

admin login: root@root.ru
admin pass: Gfhjkmroot

## Автор проекта:
[SpeedeGonzales](https://github.com/SpeedeGonzales)
