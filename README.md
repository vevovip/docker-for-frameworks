## Docker compose for frameworks

- Nginx: latest
- PHP: 7.4 / 8 (uses php-fpm)
- Postgres: 13
- Redis: 5
- MongoDB: latest
- RabbitMQ: 3-management
- XDebug: 3

### Instruction
Clone repo, copy .env.example to .env file, set params.

```
docker-compose up -d --build
```
