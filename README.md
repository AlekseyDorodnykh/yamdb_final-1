Это итоговый проект 16-го спринта.
Задача: автотест на гитхаб экшн.
Для развертывания проекта:
1.установите docker и docker-compose последней версии
2.перейдите в папку infra_sp2/infra и создайте файл .env
Шаблон для заполнения :
SECRET_KEY ='секретный ключ джанго проекта из settings.py'
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres 
POSTGRES_USER= логин_для_пользователя
POSTGRES_PASSWORD= пароль_для_пользователя
DB_HOST=db
DB_PORT=5432
DEBUG=FALSE

далее откройте терминал, перейдите в папку infra_sp2/infra и пропишите команды:
docker-compose up
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input 
если имеется бд:
положить файл .json в папку infra_sp2/api_yamdb
docker-compose exec web python manage.py loaddata NAME_OF_FILE.json


автотест:
1) проверка кода на PEP через flake8
2) проверка внутренних тестов django
3) сборка образа и пуш на докер хаб
4) деплой на рабочий сервер

при этом, необходимо добавить переменные окружения (settings в репозитории github->secrets and variables->actions)

DB_ENGINE-не обязательно-django.db.backends.postgresql
DB_HOST-не обязательно-db
DB_NAME-не обязательно-postgres
DB_PORT-не обязательно-5432
POSTGRES_PASSWORD--не обязательно-ваш пароль от бд
POSTGRES_USER-не обязательно-ваш логин от бд
DEBUG- False либо True-режим дебага в settings.py django приложения
DOCKER_PASSWORD-пароль от докер хаб
DOCKER_USERNAME-логин от докер хаб
USER-юзернейм для подключения к боевому серверу
HOST-ip адрес боевого сервера
SECRET_KEY-secret key в settings.py django приложения
SSH_KEY- ssh key вашего компьютера
TELEGRAM_TO-ваш телеграм id
TELEGRAM_TOKEN-телеграм токен вашего бота для уведомления


