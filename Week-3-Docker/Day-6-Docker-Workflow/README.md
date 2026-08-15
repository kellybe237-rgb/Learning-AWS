# Day 6 — Docker Workflow Practice

## Objective
Combine the Docker skills from the previous exercises into a repeatable workflow.

## Workflow

1. Find or pull an image.
2. Start a container.
3. Publish a port when the application needs network access.
4. Check container status.
5. Read logs.
6. Execute commands inside the container.
7. Stop/restart the container as needed.
8. Remove temporary resources when finished.

Example:

```bash
docker pull nginx
docker run -d --name web-practice -p 8080:80 nginx
docker ps
docker logs web-practice
docker exec -it web-practice /bin/bash
```

Test the published service from the EC2 host/browser, then clean up:

```bash
docker stop web-practice
docker rm web-practice
```

## Learning outcome
The goal was to move from individual Docker commands to understanding the complete container workflow.