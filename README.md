# API_YAMDB
REST API проект для сервиса YaMDb — сбор отзывов о фильмах, книгах или музыке.

## Описание

Проект YaMDb собирает отзывы пользователей на произведения.
Произведения делятся на категории: «Книги», «Фильмы», «Музыка».
Список категорий  может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
### Как запустить проект:

Все описанное ниже относится к ОС Linux.
Клонируем репозиторий и переходим в директорию api_yamdb :
```bash
git clone https://github.com/themasterid/infra_sp2
cd infra_sp2/api_yamdb
```

Создаем и активируем виртуальное окружение:
```bash
python3 -m venv venv
source /venv/Scripts/activate 
```
Ставим модули из requirements.txt:
```bash
pip install -r requirements.txt
```

Переходим в папку с файлом docker-compose.yaml:
```bash
cd infra
```

Поднимаем контейнеры (db-1, web-1, nginx-1):
```bash
docker-compose up -d --build
```

Выполняем миграции:
```bash
docker-compose exec web python manage.py makemigrations reviews
```
```bash
docker-compose exec web python manage.py migrate
```

Создаем суперпользователя:
```bash
docker-compose exec web python manage.py createsuperuser
```

Србираем статику:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```

Создаем дамп базы данных:
```bash
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```

Останавливаем контейнеры:
```bash
docker-compose down -v
```

### Пример .env файла с указанием имён переменных, которые должны быть в .env файле и их примерным/возможным содержанием смотри в файле .env.example


### Документация API YaMDb
Документация доступна по эндпойнту: http://localhost/redoc/