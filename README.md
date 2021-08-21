# Docker compose for frameworks Laravel, Symfony:

 - nginx latest
 - php-fpm 7.4
 - postgres-13.3
 - redis-5
 - mailcatcher
 - rabbitmq
 - XDebug
 - Opcache

Склонировать в корень и прописать пути в .env файле.
Запустить ```docker-compose up -d --build```

Расширения устанавливаются с помощью пакета https://github.com/mlocati/docker-php-extension-installer . 
Для установки расширения, нужно прописать в файл php-fpm.Dockerfile

В контейнере php-fpm уже установлен composer, можно установить зависимости внутри контейнера.