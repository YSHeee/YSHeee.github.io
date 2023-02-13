# Nginx + Flask + MySQL + phpMyAdmin

- Source code Reference : [awesome-compose](https://github.com/docker/awesome-compose/tree/master/nginx-flask-mysql)

```title="Structure"
.
├ docker-compose.yml
├ app
│  ├ Dockerfile
│  ├ requirements.txt
│  └ hello.py
└ proxy
│  ├ conf
│  └ Dockerfile
└ db
   └ password.txt 
```

```yaml title="docker-compose.yml"
version: '3'
services:
  db:
    image: mariadb:10-focal
    command: '--default-authentication-plugin=mysql_native_password'
    restart: always
    healthcheck:
      test: ['CMD-SHELL', 'mysqladmin ping -h 127.0.0.1 --password="$$(cat /run/secrets/db-password)" --silent']
      interval: 3s
      retries: 5
      start_period: 30s
    secrets:
      - db-password
    volumes:
      - db-data:/var/lib/mysql
    networks:
      - backnet
    environment:
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db-password
      MYSQL_DATABASE: example
    expose:
      - 3306
      - 33060
  app:
    build:
      context: app
      dockerfile: Dockerfile
    restart: always
    secrets:
      - db-password
    ports:
      - 8000:8000
    networks:
      - backnet
      - frontnet
    depends_on:
      db:
        condition: service_healthy
  proxy:
    build: 
      context: proxy
      dockerfile: Dockerfile
    restart: always
    ports:
      - 80:80
    depends_on:
      - app
    networks:
      - frontnet
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
      - 8080:8080
    secrets:
      - db-password
    networks:
      - backnet
    environment:
      PMA_ARBITRARY: 1
      PMA_HOST: db
      PMA_PORT: 3306
      PMA_USER: root
      PMA_PASSWORD_FILE: /run/secrets/db-password
    depends_on:
      db:
        condition: service_healthy

volumes:
  db-data:

secrets:
  db-password:
    file: db/password.txt

networks:
  backnet:
  frontnet:

```

---
### `localhost:8000` / `localhost:80`
![1](../images/running-5.png){: style="height:70%;width:70%"}
