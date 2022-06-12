# MYSQL база данных внутри докера

## Запуск и остановка

Чтобы не забыть: это проект для Романа Баженова чтобы он потренировался навыкам mysql.

Запускать контейнер из-под папки `deployer` так:
```bash
docker-compose up -d
```

Останавливать так:
```bash
docker-compose down
```

Проверить запущен ли контейнер можно так:
```bash
docker ps
```
Если контейнер запущен, получим что-то вроде:
```
CONTAINER ID   IMAGE             COMMAND                  CREATED         STATUS                  PORTS                                                           NAMES
8f5c24399145   mariadb:10.5.10   "docker-entrypoint.s…"   5 seconds ago   Up 4 seconds            2306/tcp, 0.0.0.0:2306->3306/tcp, :::2306->3306/tcp             mariadb_container
```
Креды для входа в файле `deployer/.env`, только host будет `localhost` или `127.0.0.1`.

Но база будет пустая. Чтобы залить в неё sql-дамп надо **из корня проекта** выполнить:

```bash
cat ФАЙЛ-ДАМПА.sql | docker exec -i КОНТЕЙНЕР ./database/bin/mysql -u ЮЗЕР --password=ПАРОЛЬ ИМЯ-БАЗЫ
```
- database/dump/ФАЙЛ-ДАМПА.sql - заменить на имя файла вашего дампа (я положил 2 тренировочные базы из сети)
- КОНТЕЙНЕР (имя докер-контейнера можно посмотреть в `deployer/.env`)
- ЮЗЕР (имя пользователя базы данных, можно посмотреть в `deployer/.env`)
- ПАРОЛЬ (пароль пользователя базы данных, можно посмотреть в `deployer/.env`)
- ИМЯ-БАЗЫ (имя базы данных, можно посмотреть в `deployer/.env`)

Для входа в БД лучше юзать: https://www.heidisql.com/download.php

А еще лучше php-шторм (тип БД - mariadb, видно в файле `docker-compose.yml`).