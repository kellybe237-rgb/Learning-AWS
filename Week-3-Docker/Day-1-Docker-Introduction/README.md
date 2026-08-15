# Day 1 — Docker Introduction

## Objective
Understand the basic Docker concepts and install Docker on an Ubuntu EC2 instance.

## Key concepts
- **Container:** An isolated process/environment for running an application.
- **Image:** A read-only template used to create containers.
- **Dockerfile:** Instructions used to build an image.
- **Docker Hub:** A registry where container images can be stored and shared.

## Installation and verification

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

Verify Docker:

```bash
docker --version
sudo docker run hello-world
```

## Add the EC2 user to the Docker group

```bash
sudo usermod -aG docker $USER
```

Log out and back in (or reconnect to the EC2 instance), then verify:

```bash
docker ps
```

## Result
Docker was installed successfully and the user was configured to run Docker without `sudo`.