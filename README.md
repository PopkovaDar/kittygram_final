### Kittygram

## Описание

Kittygram - социальная сеть в которой пользователи могут регистрироваться, делиться фотографиями своих котиков, информацией о них, и смотреть фотографии других пользователей, узнавать какие у других котиков бывают навыки и цвета шерстки.

## Как запустить проект:

# Подключение к серверу:

* Нужно зайти на сервер с помощью команды:
 ssh -i путь_до_файла_с_SSH_ключом/название_файла_закрытого_SSH-ключа login@ip
Далее вам понадобится ввести пароль от закрытого SSH-ключа (passphrase).

# Установка backend и frontend приложения:

* Клонировать репозиторий и перейти в него в командной строке:
cd kittygram_final

* Cоздать и активировать виртуальное окружение:
python3 -m venv env
source env/bin/activate

* Установить зависимости из файла requirements.txt:
python3 -m pip install --upgrade pip
pip install -r requirements.txt

* Выполнить миграции:
python3 manage.py migrate

* Соберите статику:
python3 manage.py collectstatic

* Находясь на сервере соберите статику  и зависимости frontend приложения:
npm i
npm run build
sudo cp -r путь_к_директории_с_фронтенд-приложением/build/. /var/www/имя_проекта/

* Создайте файл .env:
POSTGRES_DB='название bd'
POSTGRES_USER='указать user'
POSTGRES_PASSWORD='user пароль'
DB_NAME='указать name db'
DB_PORT='указать порт'
DB_HOST='хост db'
DEBUG='False'
ALLOWED_HOSTS='указать хосты'
SECRET_KEY='секретный ключ'
___

# Установка Gunicorn:
pip install gunicorn==20.1.0
В директории /etc/systemd/system/ создайте файл gunicorn.service и откройте его в Nano. Для создания файла в системной папке нужны права администратора, их даёт команда sudo. Выполните команду:
sudo nano /etc/systemd/system/gunicorn.service  

После небольшого ожидания можно будет проверить работоспособность запущенного демона. Для этого воспользуйтесь командой:
sudo systemctl status gunicorn
Для перезагрузки:
sudo systemctl daemon-reload

# Установка Nginx:
sudo apt install nginx -y
sudo systemctl start nginx
Используя инструкцию sudo, откройте через Nano файл конфигурации веб-сервера: 
sudo nano /etc/nginx/sites-enabled/default
Сохраните изменения, проверьте и перезагрузите конфигурацию веб-сервера:
sudo nginx -t
sudo systemctl reload nginx 
___

## Стек технологий

Django==3.2.3
djangorestframework==3.12.4
djoser==2.1.0
gunicorn==20.1.0
Nginx
Certbot

## GitHub Actions

Логика автомитизации тестирования, сборки образов проекта и их отправка на Docker Hub, перезапуска и отправки сообщения о успешном деплое по шагам описана в файле .github/workflows/main.yml workflow.


Автор [Darya](https://github.com/PopkovaDar):relaxed:
