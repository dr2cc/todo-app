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
go build && make run

```
# drk

# Запуск контейнера с db (образ postgres должен уже быть скачан).
# Со стандартным портом 5432 есть вопросы, меняем его и я (drk) его заменил в config.yml
docker run --name=todo-db -e POSTGRES_PASSWORD=qwerty -p 5436:5432 -d --rm postgres

# Если приложение запускается впервые, необходимо применить миграции к базе данных:
## Применение схемы миграции. Миграции это как система контроля версий для db
migrate -path ./schema -database 'postgres://postgres:qwerty@localhost:5436/postgres?sslmode=disable' up

# hash Получение в конце видео №6
686a7172686a7177313234363137616a6668616a73b1b3773a05c0ed0176787a4f1574ff0075f7521e

# Настройка Swagger для проекта на Golang
https://youtu.be/DBZgt9iIWzk?t=641
9:30

[Документация swagger в нашем проекте](http://localhost:8000/swagger/index.html)

# Установка swagger
go install github.com/swaggo/swag/cmd/swag@latest

# После запускаем из корня, но ссылаясь на main.go
# Так создается документация.
swag init -g .\cmd\main.go

# Была ошибка в import файла handler.go . Два варианта решения:
# Написать:
import (
	swaggerFiles "github.com/swaggo/files"
	ginSwagger "github.com/swaggo/gin-swagger"
)

# или в начале закомментировать хендлер 
# // router.GET("/swagger/*any", ginSwagger.WrapHandler(swaggerFiles.Handler))
# Написать :
import (
	"github.com/swaggo/gin-swagger"
    "github.com/swaggo/files"
)
# а после снять комментарий с хендлера и сохранить.


# 9 5:00

# 5 
## Один раз, импорт. Позволяет читать .env
go get -u github.com/joho/godotenv

## Один раз, создать в корне файл .env с данными:
DB_PASSWORD=qwerty

# 4
## Если нужен откат таблиц db с текущей версии на предыдущую
migrate -path ./schema -database 'postgres://postgres:qwerty@localhost:5436/postgres?sslmode=disable' down


## Состояние docker, из него берем CONTAINER ID, в этот раз 6f02c8402d0b
docker ps
## Подключение к db в контейнере 6f02c8402d0b
docker exec -it 6f02c8402d0b /bin/bash

## Комманды linux
psql -U postgres

select * from users;
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