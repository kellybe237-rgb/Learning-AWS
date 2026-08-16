# Week 3 — Docker 🐳

This week focused on learning Docker on an **Ubuntu EC2 instance**, progressing from the fundamentals to containerized applications and advanced Docker features.

## Week 3 objectives

- Understand Docker containers, images, Dockerfiles, and registries.
- Install and verify Docker on Ubuntu EC2.
- Run and manage containers from the command line.
- Pull, inspect, build, tag, and manage Docker images.
- Build and deploy a custom web application image.
- Publish container ports and verify applications from a browser.
- Practice Docker Swarm and service management.
- Use Docker Compose to deploy a multi-container WordPress + MySQL application.
- Explore advanced Docker topics such as volumes, networks, environment variables, and resource inspection.

---

## Exercises completed

| Day | Topic | Result |
|---|---|---|
| 1 | Docker Introduction | Docker installed and verified on Ubuntu EC2 |
| 2 | Docker Images | Images pulled, inspected, and custom image built |
| 3 | Docker Containers | Container lifecycle practiced |
| 4 | Nginx | Nginx container published and custom web page verified |
| 5 | Docker Management | Containers, images, logs, and cleanup practiced |
| 6 | Docker Workflow | Complete image → container → test → cleanup workflow practiced |
| 7 | Advanced Docker | Swarm, services, Compose, volumes/networks, and multi-container applications explored |

---

# 1. Docker installation and verification

Installed Docker on an Ubuntu EC2 instance and enabled the Docker service.

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

Configured the Ubuntu user to run Docker without `sudo`:

```bash
sudo usermod -aG docker $USER
```

Verified the installation with:

```bash
docker --version
docker run hello-world
docker ps
```

### Result

The Docker `hello-world` container ran successfully and confirmed that the Docker client, daemon, image pull, and container runtime were working correctly.

---

# 2. Docker images and custom image building

Practiced working with Docker images:

```bash
docker pull nginx
docker images
docker image ls
docker image inspect nginx
```

Also practiced removing unused images:

```bash
docker rmi nginx
```

## Custom Docker web image

Created a simple HTML page and a Dockerfile based on Nginx.

Example Dockerfile:

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
```

Built the image:

```bash
docker build -t my-web-app .
```

Verified the image:

```bash
docker images
```

Ran it as a container:

```bash
docker run -d --name my-web-container -p 80:80 my-web-app
```

Verified the application from the EC2 host:

```bash
curl http://localhost
```

The custom page displayed:

> **Hello from my Docker container!**

This demonstrated the complete process of creating application content, packaging it into a Docker image, running the image as a container, and exposing it through HTTP.

---

# 3. Running and managing containers

Practiced the Docker container lifecycle:

```bash
docker run -d --name my-nginx nginx
docker ps
docker logs my-nginx
docker logs -f my-nginx
docker exec -it my-nginx /bin/bash
docker stop my-nginx
docker start my-nginx
docker rm my-nginx
```

Also used inspection commands:

```bash
docker ps -a
docker inspect my-nginx
docker stats
```

### Result

I learned how to create, inspect, access, monitor, stop, restart, and remove Docker containers.

---

# 4. Nginx container and browser verification

Ran Nginx with a published port:

```bash
docker run -d --name my-nginx -p 80:80 nginx
```

The container's default web content is stored at:

```text
/usr/share/nginx/html/index.html
```

After modifying the page, I verified the result from a browser using the EC2 instance's public IP address.

This helped connect Docker port publishing with real network access:

```text
EC2 public IP : 80  →  Docker container : 80
```

---

# 5. Docker Swarm

Created a Docker Swarm manager on an Ubuntu EC2 instance:

```bash
docker swarm init
```

Verified Swarm mode:

```bash
docker info | grep Swarm
docker node ls
```

The node was shown as the **Leader/Manager**.

Created an Nginx Swarm service:

```bash
docker service create --name my-nginx --publish published=8080,target=80 nginx
```

Verified the service:

```bash
docker service ls
docker service ps my-nginx
```

### Result

The Nginx service reached the **Running** state, demonstrating the basic Docker Swarm workflow of initializing a cluster and deploying a service.

---

# 6. Docker Compose — WordPress + MySQL

Created a multi-container WordPress environment using Docker Compose.

The application contained two services:

- **wordpress-app** — WordPress application
- **wordpress-db** — MySQL database

The Compose deployment created:

- A Docker network for the application
- A persistent database volume
- A WordPress container
- A MySQL container

Started the application with:

```bash
docker compose up -d
```

Verified the containers:

```bash
docker compose ps
docker ps
```

The containers were running and WordPress was accessible through the published port:

```text
EC2 public IP : 8080 → WordPress : 80
```

I then reached the WordPress installation page in the browser.

### Result

This exercise demonstrated how Docker Compose can coordinate multiple containers that work together as one application stack.

> Note: Docker Compose may display a warning if the Compose file contains the older top-level `version:` attribute. Modern Compose ignores this attribute, so it can be removed from the file.

---

# 7. Advanced Docker topics

Additional topics practiced during the week included:

### Environment variables

```bash
docker run --rm -e APP_ENV=development nginx env
```

### Volumes

```bash
docker volume ls
docker volume create demo-data
docker volume inspect demo-data
```

### Networks

```bash
docker network ls
docker network create demo-network
```

### Resource inspection

```bash
docker inspect <container>
docker stats <container>
docker top <container>
```

These exercises helped reinforce the difference between containers, persistent data, networks, and runtime configuration.

---

# Hands-on evidence

The Week 3 exercises were completed on Ubuntu EC2 and verified through terminal output and browser testing.

Evidence captured during the exercises includes:

1. Docker installation and successful `hello-world` execution.
2. Custom Docker image creation and browser verification.
3. Docker image listing, container management, and `curl` verification.
4. Docker Swarm initialization and an Nginx service reaching the Running state.
5. Docker Compose starting WordPress and MySQL.
6. Verification that the WordPress and MySQL containers were running.
7. WordPress installation page successfully reached in the browser.

These screenshots document the practical results of the Week 3 work and complement the command examples in the daily exercise folders.

---

# Skills gained

- Docker fundamentals
- Docker CLI
- Docker images
- Dockerfiles
- Docker Hub / image registries
- Container lifecycle management
- Nginx containers
- Port publishing
- Custom Docker image creation
- Docker Swarm
- Docker services
- Docker Compose
- Multi-container applications
- WordPress + MySQL containerization
- Docker volumes
- Docker networks
- Environment variables
- Container inspection and troubleshooting
- Running Docker on AWS EC2

---

# Key takeaway

Week 3 moved my learning from basic AWS infrastructure into **containerization and application deployment**. I learned how to package applications into Docker images, run and manage containers, expose applications through network ports, create Swarm services, and deploy a multi-container WordPress application with Docker Compose.

This provides a strong foundation for the next stage of cloud learning, including container orchestration, CI/CD, and deploying containerized workloads on AWS.
