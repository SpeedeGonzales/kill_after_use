## Описание проекта

Проект Kittygram реализует сервис для публикации фото котиков, описание их достижений с возможностью редактирования и просмотра другими пользователями.

## Запуск приложения в Ubuntu/Debian Linux

Установка и запуск приложения на сервер возможна в двух вариантах. Из исходных кодов на Github вручную и c использованием CI/CD GitHub Actions

### Из исходных кодов GitHub

1. Создать на сервере в домашнем каталоге каталог `kittygram`:

```
$ mkdir kittygram
```

2. Клонировать репозиторий:

```bash 
$ git clone git@github.com:SpeedeGonzales/kittygram_final.git
```

3. В корневом каталоге проекта из файла `.env.example` создать файл `.env`, при необходимости заменив значения переменных.

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

5. Запустить в каталоге `kittygram` Docker Compose в режиме демона:
```
$ sudo docker compose up -d
```
В результате соберутся и запустятся необходимые контейнеры.

6. Выполнить следующие команды:
```
$ sudo docker compose exec backend python manage.py migrate
$ sudo docker compose exec backend python manage.py collectstatic
$ sudo docker compose exec backend cp -r /app/collected_static/. /backend_static/static/
```

7. Установить согласно документации Nginx. В конфигурационном файле `/etc/nginx/sites-enabled/default` в секции `server` изменить настройки `location`:

```
location / {
    proxy_set_header Host $http_host;
    proxy_pass http://127.0.0.1:9000;
}
```

8. Перезапустить Nginx:

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

## Используемые технологии

- Python
- Django
- Django REST framework
- Node.js
- Docker
- PostgreSQL
- Nginx

## Создатель проекта:
* [SpeedeGonzales]([https://github.com/SpeedeGonzales])
