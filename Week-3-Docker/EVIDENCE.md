# Week 3 Docker — Hands-on Evidence 📸

The following screenshots were captured while completing the Week 3 Docker exercises on Ubuntu EC2.

> The screenshots document terminal output and browser verification from the actual practice sessions.

## Evidence 1 — Docker installation and `hello-world`

**What it proves:** Docker was installed and the Docker engine successfully pulled and ran the `hello-world` image.

Key commands shown during the exercise:

```bash
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
docker run hello-world
```

## Evidence 2 — Custom Docker web application

**What it proves:** A custom Docker image was built from a Dockerfile and used to serve custom HTML through Nginx.

The browser displayed:

> Hello from my Docker container!

## Evidence 3 — Image and container verification

**What it proves:** Docker images and running containers were inspected, and the custom application was verified with `curl`.

Example commands:

```bash
docker images
docker ps
docker run -d --name my-web-container -p 80:80 my-web-app
curl http://localhost
```

## Evidence 4 — Docker Swarm

**What it proves:** Docker Swarm was initialized and an Nginx service was deployed successfully.

Example commands:

```bash
docker swarm init
docker node ls
docker service create --name my-nginx --publish published=8080,target=80 nginx
docker service ls
docker service ps my-nginx
```

The service reached the **Running** state.

## Evidence 5 — Docker Compose WordPress + MySQL

**What it proves:** Docker Compose created and started the WordPress application and MySQL database containers.

Example command:

```bash
docker compose up -d
docker compose ps
```

## Evidence 6 — Container verification

**What it proves:** Both `wordpress-app` and `wordpress-db` were running successfully.

## Evidence 7 — WordPress installation page

**What it proves:** The containerized WordPress application was reachable through the EC2 public IP and the WordPress installation process was successfully reached in a browser.

## Skills demonstrated

- Docker installation on Ubuntu EC2
- Docker image management
- Dockerfile and custom image creation
- Container lifecycle management
- Nginx container deployment
- Port publishing
- Browser and `curl` verification
- Docker Swarm and services
- Docker Compose
- WordPress + MySQL multi-container deployment
- Volumes and networks
- Container troubleshooting and verification
