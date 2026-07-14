**Docker Compose** is a tool for running multiple Docker containers using one configuration file.

Define how to run multiple Docker containers in `docker-compose.yaml`.
```yml
services:
  web:
    image: nginx
    ports:
      - "8080:80"

  redis:
    image: redis
```

Build images.
```shell
docker compose -f docker-compose.yaml build
```

Start containers.
```shell
docker compose -f docker-compose.yaml up -d
```
Options:
- `-d`: **Detached mode.** Run the containers in the background.

Stop and restart containers.
```shell
docker compose -f docker-compose.yaml stop
docker compose -f docker-compose.yaml start
```

Stop and remove containers.
```shell
docker compose -f docker-compose.yaml down
```