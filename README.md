## Описание проекта

Проект Kittygram реализует сервис для публикации фото котиков, описание их достижений с возможностью редактирования и просмотра другими пользователями.

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
sudo docker compose exec backend python manage.py migrate
sudo docker compose exec backend python manage.py collectstatic
sudo docker compose exec backend cp -r /app/collected_static/. /backend_static/static/
```
