# Руководство по настройке Docker-compose

Этот проект создан для выполнения практического задания №4 по работе с Docker-compose.

## Описание

Работа включает в себя клонирование репозитория исходных файлов [docker-nginx-python2-db-redis-homework](https://github.com/darkbenladan/docker-nginx-python2-db-redis-homework), проверку конфигурационных файлов, Dockerfile и docker-compose.yml на наличие ошибок, а также их исправление в соответствии с указанными требованиями.

## Инструкции

### Шаг 1: Клонирование репозитория

```bash
git clone https://github.com/darkbenladan/docker-nginx-python2-db-redis-homework.git
```

### Шаг 2: Исправление Dockerfile

В папке `web` внесите следующие изменения в файл `Dockerfile`:

```Dockerfile
# Задаем источник python:2.7-stretch
FROM python:2.7-stretch

# Задаем пользователя root
USER root

# Задаем порт 9000
EXPOSE 9000
```

### Шаг 3: Исправление docker-compose.yml

В файле `docker-compose.yml` внесите следующие изменения:

```yaml
services:
  ...
  # Определение сетей
  networks:
    - frontend
    - backend

  ...
  # Добавление пути для volume
  volumes:
    - ./web/cron/crontab_todo:/etc/crontab

  ...
  # Добавление порта 9000 в блок consumers
  consumers:
    ports:
      - "9000:9000"

  ...
  # Добавление пути для build и порта 6379 в блок redis
  redis:
    build: ./redis
    ports:
      - "6379:6379"

networks:
  frontend:
  backend:
```

### Шаг 4: Запуск Docker-compose

```bash
docker-compose up
```
