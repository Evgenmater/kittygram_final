### Описание проекта:

Kittygram — социальная сеть для обмена фотографиями любимых питомцев.
Новые пользователи могут самостоятельно регистрироваться в нашем сервисе. Так же добавлять, обновлять и удалять информацию о своих котиках.


### Как запустить проект:

* Клонировать репозиторий и перейти в него в командной строке:

    ```
    git clone git@github.com:Evgenmater/kittygram_final.git
    ```

* Перейти в директорию проекта:

    ```
    cd kittygram_final
    ```

* Cобираем образы, замените "usernmae" на ваш логин на Docker Hub:

    ```
    cd frontend
    docker build -t username/kittygram_frontend .
    cd ../backend
    docker build -t username/kittygram_backend .
    cd ../nginx
    docker build -t username/kittygram_gateway .
    ```

* Загружаем образы на Docker Hub, замените "usernmae" на ваш логин на Docker Hub:

    ```
    docker push username/kittygram_frontend
    docker push username/kittygram_backend
    docker push username/kittygram_gateway
    ```

* В конфиге docker-compose.production.yml, замените "evgenmater" на ваш логин на Docker Hub:

    ```
    image: evgenmater/kittygram_backend
    ```

* Запустите Docker Compose с этой конфигурацией на своём компьютере, далее команды, чтобы собрать статику:

    ```
    docker compose -f docker-compose.production.yml up
    docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
    docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/
    ```

* Выполнить миграции:

    ```
    docker compose -f docker-compose.production.yml exec backend python manage.py migrate
    ```

### Примеры запросов к API.

* Получить список всех котиков:

    ```
    https://yakittygram.myftp.org/api/сats/
    ```

* Получение конкретного котиков:

    ```
    https://yakittygram.myftp.org/api/сats/1/
    ```

* Получение список всех котиков у конкретного пользователя:

    ```
    https://yakittygram.myftp.org/api/users/
    ```
