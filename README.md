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

## Запуск приложения

Запуск приложения возможен в двух вариантах. Из исходных кодов на Github и c использованием CI/CD GitHub Actions

### Из исходных кодов GitHub

1. Клонировать репозиторий:

```bash 
git clone git@github.com:SpeedeGonzales/kittygram_final.git
```
2. В корневом каталоге проекта из файла `.env.example` создать файл `.env`, при необходимости заменив значения переменных.

```bash 
cp .env.example .env
```

Выполняем запуск:

```bash
sudo docker compose -f docker-compose.yml up
```

## После запуска: Миграции, сбор статистики

После запуска необходимо выполнить сбор статистики и миграции бэкенда. Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается. 

```bash
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/
```

И далее проект доступен на: 

```
http://localhost:9000/
```



