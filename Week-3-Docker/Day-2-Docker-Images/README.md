# Day 2 — Working with Docker Images

## Objective
Learn how to download, inspect, manage, and build Docker images.

## Pull an image

```bash
docker pull nginx
docker images
```

## Inspect images

```bash
docker image ls
docker image inspect nginx
```

## Remove an image

```bash
docker rmi nginx
```

If a container is still using the image, remove the container first.

## Build a custom image

Example `Dockerfile`:

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY . .
RUN pip install --no-cache-dir flask
EXPOSE 5000
CMD ["python", "app.py"]
```

Build it:

```bash
docker build -t my-python-app .
```

Run it:

```bash
docker run -d -p 5000:5000 --name my-python-app my-python-app
```

## Practice
Create a simple web application, package it into a Docker image, build the image, and run it as a container.