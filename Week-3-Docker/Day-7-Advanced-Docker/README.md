# Day 7 — Optional Advanced Docker Topics

## Objective
Explore additional Docker features after learning the core image and container workflow.

## Container naming and detached execution

```bash
docker run -d --name advanced-nginx nginx
docker ps
```

## Environment variables

```bash
docker run --rm -e APP_ENV=development nginx env
```

## Port publishing

```bash
docker run -d --name advanced-web -p 8080:80 nginx
```

## Resource and runtime inspection

```bash
docker inspect advanced-web
docker stats advanced-web
docker top advanced-web
```

## Volumes

Docker volumes provide persistent storage independent of a container's writable layer.

```bash
docker volume ls
docker volume create demo-data
docker volume inspect demo-data
```

## Networking

```bash
docker network ls
docker network create demo-network
```

A container can be attached to the network with `--network demo-network`.

## Cleanup

```bash
docker rm -f advanced-nginx advanced-web
docker volume rm demo-data
docker network rm demo-network
```

## Learning outcome
The advanced exercise introduced practical Docker features including environment variables, port mapping, resource inspection, volumes, and custom networks.