# Day 3 — Running and Managing Containers

## Objective
Practice the Docker container lifecycle and learn how to interact with running containers.

## Run a container

```bash
docker run -d --name my-nginx nginx
docker ps
```

## View logs

```bash
docker logs my-nginx
docker logs -f my-nginx
```

## Enter a running container

```bash
docker exec -it my-nginx /bin/bash
```

Exit the container shell with:

```bash
exit
```

## Stop and start

```bash
docker stop my-nginx
docker start my-nginx
```

## Remove the container

```bash
docker stop my-nginx
docker rm my-nginx
```

## Useful inspection commands

```bash
docker ps
docker ps -a
docker inspect my-nginx
docker stats
```

## Result
The container lifecycle was practiced from creation through logs, interactive access, stopping, restarting, and removal.