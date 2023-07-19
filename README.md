### Модуль G4.10 Итоговое задание
#### выполнил Пригон Максим FPW-82
***
1. для запуска образов необходимы docker и docker-compose
sudo apt install docker-compose -y

2.Development

Запуск из корневого каталога проекта django-on-docker-v2
Создать образ, контейнеры и запустить:
docker-compose up -d –build

Используется Django server, Postgres
Суперпользователь admin, пароль admin создается вместе с образом
Доступ к серверу:
http://localhost:8000
http://localhost:8000/admin

Доступ к Postgres:
docker-compose exec db psql --username=hello_django --dbname=hello_django_dev
Ввести команды: \list, \dt

Останавливаем и удаляем два контейнера development, volumes и один образ development
docker-compose down -v
docker images
docker rmi <image ID>

3. Production

Используется Django, Gunicorn, Nginx, Postgres

sudo docker-compose -f docker-compose.prod.yml up -d –build
Суперпользователь admin, пароль admin создается вместе с образом

Сервер nginx
http://localhost:1337/
Доступна функция загрузки изображений, можно загрузить, а потом посмотреть
http://localhost:1337/admin

Доступ к Postgres:
Проверить volume:
docker volume inspect django-on-docker-v2_postgres_data
Открыть доступ к базе:
docker-compose exec db psql --username=hello_django --dbname=hello_django_prod
Ввести команды: \list, \dt

Остановить и удалить контейнеры, тома Production
docker-compose -f docker-compose.prod.yml down -v
