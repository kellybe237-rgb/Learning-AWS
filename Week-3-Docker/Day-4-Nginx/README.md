# Day 4 — Nginx Container Exercise

## Objective
Run Nginx in Docker, publish it to a host port, modify its default HTML page, and verify the result in a browser.

## Run Nginx

```bash
docker run -d --name my-nginx -p 80:80 nginx
docker ps
```

The `-p 80:80` option maps port 80 on the EC2 host to port 80 inside the container.

## Access the container

```bash
docker exec -it my-nginx /bin/bash
```

The default Nginx page is located at:

```text
/usr/share/nginx/html/index.html
```

Inspect it:

```bash
cat /usr/share/nginx/html/index.html
```

## Modify the page

For the exercise, replace the default page with a simple custom HTML page. After changing it, verify the result from a browser using the EC2 instance's public address.

## Verify from Docker

```bash
docker logs my-nginx
docker ps
```

## Cleanup

```bash
docker stop my-nginx
docker rm my-nginx
```

## Result
An Nginx container was published to the EC2 host and its default web page was customized and tested.