# Day 5 — Docker Management Practice

## Objective
Strengthen everyday Docker administration skills.

## Container and image inventory

```bash
docker ps
docker ps -a
docker images
```

## Useful lifecycle workflow

```bash
docker run -d --name practice-nginx nginx
docker logs practice-nginx
docker exec -it practice-nginx /bin/bash
docker stop practice-nginx
docker start practice-nginx
docker rm -f practice-nginx
```

## Inspect Docker resources

```bash
docker image ls
docker container ls -a
docker system df
```

## Cleanup unused resources

Use cleanup commands carefully because they can remove resources that are no longer in use:

```bash
docker system prune
```

## Practice goal
Become comfortable reading Docker state, identifying running versus stopped containers, checking logs, entering containers, and cleaning up test resources.