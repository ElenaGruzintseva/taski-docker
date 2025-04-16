
![Workflow Status](https://github.com/ElenaGruzintseva/taski-docker/actions/workflows/main.yml/badge.svg)

Проект доступен по адресу: https://taskitaski.hopto.org/

# Taski

Taski - небольшой сервис для хранения задач и отметок об их выполнении.

 - Создать задачу
 - Отметить задачу как выполненную


## Стек технологий
 - Django
 - DRF
 - PyYAML
 - Nginx
 - Docker Compose
 - GitHub Actions

### Как развернуть проект локально

Убедитесь, что на вашем компьютере установлены Docker и Docker Compose.

Клонируйте репозиторий:

```
git clone https://github.com/ElenaGruzintseva/taski-docker
cd taski-docker
```

Создайте файл .env и добавьте необходимые переменные окружения. Пример:

```
SECRET_KEY='default-secret-key'
DEBUG=True
ALLOWED_HOSTS='127.0.0.1, localhost'
POSTGRES_USER=django_user
POSTGRES_PASSWORD=django_password
POSTGRES_DB=django
DB_HOST=db
DB_PORT=5432
```

Запустите Docker Compose для создания и запуска контейнеров:

```
sudo docker-compose up -d
```

В контейнере taski-docker-backend примените миграции, соберите статику:

```
sudo docker compose exec backend python manage.py migrate
sudo docker compose exec backend python manage.py collectstatic
```

Проект будет доступен здесь http://localhost:8000

### Для автоматизации развертывания проекта используйте GitHub Actions

Добавьте секреты в репозиторий:

```
DOCKER_PASSWORD - пароль от Docker Hub
DOCKER_USERNAME - имя пользователя Docker Hub
HOST - ip сервера
USER - имя пользователя сервера
SSH_KEY - ключ ssh для доступа к удаленному серверу
SSH_PASSPHRASE - пароль ssh
TELEGRAM_TO - id пользователя TELEGRAM
TELEGRAM_TOKEN - TELEGRAM токен для отправки сообщений
```

В файле docker-compose.production.yml замените username для всех образов на свой, например:

```
image: yourusername/taski_backend
image: yourusername/taski_frontend
image: yourusername/taski_gateway
```

При каждом пуше в ветку main сработает main.yml.

После успешного выполнения workflow, образы будут опубликованы на DockerHub,
в Telegram будут отправлены сообщения об успешном деплое,
проект будет доступен по вашему ip, указанному в секретах.


### [ElenaGruzintseva](https://github.com/ElenaGruzintseva)
