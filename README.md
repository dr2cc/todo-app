# REST API Для Создания TODO Списков на Go

## <a href="https://www.youtube.com/playlist?list=PLbTTxxr-hMmyFAvyn7DeOgNRN8BQdjFm8">Видеокурс на YouTube</a>

## В курсе разобранны следующие концепции:
- Разработка Веб-Приложений на Go, следуя дизайну REST API.
- Работа с фреймворком <a href="https://github.com/gin-gonic/gin">gin-gonic/gin</a>.
- Подход Чистой Архитектуры в построении структуры приложения. Техника внедрения зависимости.
- Работа с БД Postgres. Запуск из Docker. Генерация файлов миграций. 
- Конфигурация приложения с помощью библиотеки <a href="https://github.com/spf13/viper">spf13/viper</a>. Работа с переменными окружения.
- Работа с БД, используя библиотеку <a href="https://github.com/jmoiron/sqlx">sqlx</a>.
- Регистрация и аутентификация. Работа с JWT. Middleware.
- Написание SQL запросов.
- Graceful Shutdown

### Для запуска приложения:

```
make build && make run
```

### Если приложение запускается впервые, необходимо применить миграции к базе данных:

```
make migrate
```
# drk

# Запуск контейнера (из скачанного образа) с db, образ postgres должен уже быть скачан
docker run --name=todo-db -e POSTGRES_PASSWORD=qwerty -p 5436:5432 -d --rm postgres
# Применение схемы миграции. Миграции это как система контроля версий для db
migrate -path ./schema -database 'postgres://postgres:qwerty@localhost:5436/postgres?sslmode=disable' up

# 9 5:00

# 5 
## Один раз, импорт. Позволяет читать .env
go get -u github.com/joho/godotenv

## Один раз, создать в корне файл .env с данными:
DB_PASSWORD=qwerty

# 4
## Если нужен откат таблиц db с текущей версии на предыдущую
migrate -path ./schema -database 'postgres://postgres:qwerty@localhost:5436/postgres?sslmode=disable' down


## Состояние docker, из него берем CONTAINER ID, в этот раз 0bc0d399a43c
docker ps
## Подключение к db в контейнере 0bc0d399a43c
docker exec -it 0bc0d399a43c /bin/bash

## Комманды linux
psql -U postgres
\d
exit
exit

# =====-*-=======
## (скачивание образа postgres в docker)
docker pull postgres

# About  the migration utilite on windows.

<a href="https://github.com/golang-migrate/migrate/tree/master/cmd/migrate">migrate</a>

# Install scoop:

Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

scoop install migrate

# Делается если в репозитории нет схем миграции. Создание структур миграции, утилита migrate к этому моменту должна быть установлена
migrate create -ext sql -dir ./schema -seq init