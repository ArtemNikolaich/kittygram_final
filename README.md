# Kittygram

## Описание проекта

**Kittygram** - это веб-приложение для обмена фотографиями котиков. Пользователи могут загружать свои снимки котиков и просматривать фотографии, размещенные другими пользователями.
Разворачивание проекта
## Следуйте этим шагам, чтобы развернуть проект на сервере:

**Установите Docker и Docker Compose на ваш сервер:**
```
sudo apt update
```
```
sudo apt install curl
```
```
curl -fsSL https://get.docker.com -o get-docker.sh
```
```
sudo sh get-docker.sh
```
```
sudo apt-get install docker-compose
```
**Склонируйте репозиторий проекта:**
```
git clone git@github.com:ArtemNikolaich/kittygram_final.git
```
**Запустите проект с помощью Docker Compose:**
```
sudo docker-compose -f docker-compose.production.yml up -d
```
**Выполните миграции и соберите статические файлы:**
```
sudo docker-compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker-compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker-compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/
```
**Настройте Nginx:**
```
sudo docker-compose -f docker-compose.production.yml exec nginx nginx -s reload
```
**В файле конфигурации Nginx `(nginx.conf)` измените настройки location:**
```
location / {
    proxy_pass http://127.0.0.1:ВАШ_ПОРТ;
}
```
**Проверьте корректность конфигурации Nginx:**
```
sudo nginx -t
```
**Перезапустите Nginx:**
```
sudo service nginx reload
```
## Описание переменных окружения

**Для работы приложения необходимо установить следующие переменные окружения в файле `.env`:**

- `SECRET_KEY`: Секретный ключ Django для обеспечения безопасности приложения.
- `DEBUG`: Установите значение `True` для режима разработки и отладки приложения, и `False` для режима продакшена.
- `ALLOWED_HOSTS`: Список разрешенных хостов, разделенных запятыми.
- `POSTGRES_USER`: Имя пользователя
- `POSTGRES_PASSWORD`: Пароль базы данных
- `POSTGRES_DB`: Имя базы данных
- `DB_HOST`: Имя хоста базы данных
- `DB_PORT`: Порт базы данных

**Пример файла `.env`:**

- `SECRET_KEY`=my_secret_key
- `DEBUG`=True
- `ALLOWED_HOSTS`=your_domain_or_ip,localhost,127.0.0.1
- `POSTGRES_DB`=project_name
- `POSTGRES_USER`=project_user
- `POSTGRES_PASSWORD`=project_password
- `DB_HOST`=db
- `DB_PORT`=****
## Настройка CI/CD
**Для настройки CI/CD в GitHub Actions, добавьте следующие секреты:**

- `DOCKER_PASSWORD`: пароль от DockerHub
- `DOCKER_USERNAME`: логин от DockerHub
- `HOST`: ip адрес сервера
- `USER`: имя пользователя на сервере
- `SSH_KEY`: приватный ключ для подключения к серверу
- `SSH_PASSPHRASE`: пароль от приватного ключа
- `TELEGRAM_TO`: id пользователя в Telegram
- `TELEGRAM_TOKEN`: токен бота в Telegram

## Используемые технологии

![](https://camo.githubusercontent.com/322390071e070cfd75db97f646ff9878e45f22306a90d7682e49da86402d8f54/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4e6f64654a532d3430343133373f7374796c653d666f722d7468652d6261646765266c6f676f3d4e6f64652e4a53266c6f676f436f6c6f723d383363643239)![](https://camo.githubusercontent.com/8bfae175a07d3f8b6e55e134c9ef6d6dc3307ba144fa1162c981313ec59fffc1/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446a616e676f2d3130336532653f7374796c653d666f722d7468652d6261646765266c6f676f3d446a616e676f266c6f676f436f6c6f723d7768697465)![](https://camo.githubusercontent.com/c5726bd71e0eb47e7a9c8740c94351f2229908bab71dfd23083e8205c3443def/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f507974686f6e2d3330333633643f7374796c653d666f722d7468652d6261646765266c6f676f3d507974686f6e266c6f676f436f6c6f723d79656c6c6f77)![](https://camo.githubusercontent.com/dad46ec2dae95e1fffa2749d787ae49b18f7da0f271f728405ef5974a639e912/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f506f7374677265732d3333363739313f7374796c653d666f722d7468652d6261646765266c6f676f3d506f737467726573716c266c6f676f436f6c6f723d7768697465)![](https://camo.githubusercontent.com/607f5f48387c389e7ea1206a02530235cbae93b1e1fd3bf374c4ae9401fce2de/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f636b65722d3234393665643f7374796c653d666f722d7468652d6261646765266c6f676f3d646f636b6572266c6f676f436f6c6f723d7768697465)
  
## Автор

- `Автор`: Калинин Артём
- `GitHub`: [ArtemNikolaich](https://github.com/ArtemNikolaich)
- `Email`: artyom.kalinin.tc@gmail.com



