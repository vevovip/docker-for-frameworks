# docker-for-frameworks

Склонировать в корень

Зайти в папку и запустить ```docker-compose up -d build```

Расширения устанавливаются с помощзью пакета https://github.com/mlocati/docker-php-extension-installer . 
Для установки расширения, нужно прописать в файл php-fpm.docker

В контейнере php-fpm уже установлен composer, можно установить зависимости внутри контейнера, команда:
```composer install --ignore-platform-reqs```