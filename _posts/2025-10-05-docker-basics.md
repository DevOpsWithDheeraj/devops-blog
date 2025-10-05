---
layout: post
title: "Docker Basics"
date: 2025-10-05
---

Docker is a platform that allows you to build, ship, and run applications in lightweight, portable containers, ensuring consistency across environments.

---

## 1. Introduction to Docker
Docker is a platform for developing, shipping, and running applications in lightweight, portable containers. Containers package an application and all its dependencies together, ensuring it runs consistently across environments.

Why Docker?
Environment consistency (Dev, QA, Prod)
Lightweight and fast compared to VMs
Easy application scaling
Simplified CI/CD integration

## 2. Docker Architecture
Docker has three main components:
1. Docker Engine: Core service that manages containers.
2. Docker Images: Read-only templates for containers (like snapshots of an app environment).
3. Docker Containers: Running instances of Docker images.
4. Docker Registry: Repository for storing images (Docker Hub is the public registry).

High-level flow:
```rust
Dockerfile -> Docker Image -> Docker Container
```

## 3. Installing Docker
### Linux (Ubuntu example):
```bash
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER   # Run docker without sudo
```
### Check installation:
```bash
docker --version
docker info
```

## 4. Docker Basic Commands
### 4.1 Images
```bash
docker images   # List images
docker pull ubuntu:latest   # pull image
docker rmi ubuntu:latest    # remove image
```
### 4.2 Containers
```bash
docker run -it ubuntu:latest /bin/bash    # run container
docker ps    # List running containers
docker ps -a   # List all containers
docker stop <container_id>  # Stop a container
docker rm <container_id>   # Remove a container
docker start -ai <container_id>   # Start a container again
```
## 5. Dockerfile Basics
A Dockerfile is a text file containing instructions to build a Docker image.
### Example:
```dockerfile
# Base image
FROM ubuntu:latest

# Maintainer info
LABEL maintainer="dheeraj@example.com"

# Install packages
RUN apt-get update && apt-get install -y python3 python3-pip

# Copy app files
COPY app.py /app/app.py

# Set working directory
WORKDIR /app

# Run the app
CMD ["python3", "app.py"]
```

## 6. Docker Networking
1. Bridge (default): Isolated network; containers can communicate.
2. Host: Shares host network.
3. Overlay: Used in Docker Swarm for multi-host networking.
### Inspect network:
```bash
docker network ls
docker network inspect bridge
```
### Connect container to network:
```bash
docker network connect <network_name> <container_id>
```
## 7. Docker Volumes
Volumes persist data beyond container lifecycle.
```bash
docker volume create myvol   #Create volume:
docker run -v myvol:/data ubuntu   # Mount volume in container
docker volume ls   # List volumes
```
## 8. Docker Compose
Docker Compose allows multi-container applications with a single YAML file.
### docker-compose.yml example:
```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
  app:
    image: my-python-app
    volumes:
      - ./app:/app
```

### commands:
```
docker-compose up
docker-compose down
docker-compose logs
```

## 9. Docker Registry
### Push image to Docker Hub:
```
docker login
docker tag my-python-app username/my-python-app:latest
docker push username/my-python-app:latest
```
### Pull image from Docker Hub:
```
docker pull username/my-python-app:latest
```

## 10. Advanced Docker Concepts
### 10.1 Multi-Stage Builds
Optimizes image size by separating build and runtime environments.
```dockerfile
# Stage 1: build
FROM golang:1.20 as builder
WORKDIR /app
COPY . .
RUN go build -o app

# Stage 2: runtime
FROM alpine:latest
COPY --from=builder /app/app /app/app
CMD ["/app/app"]
```
### 10.2 Docker Swarm
1. Native Docker orchestration tool
2. Manage multi-container apps across multiple nodes
```
docker swarm init
docker service create --name myservice -p 80:80 nginx
docker service ls
```
### 10.3 Docker Security
1. Use minimal base images (Alpine)
2. Scan images for vulnerabilities
3. Run containers with non-root user

### 10.4 Docker Logging
```
docker logs <container_id>   # View logs
docker logs -f <container_id>   # Stream logs
```

## 11. Docker Best Practices
1. Use .dockerignore to reduce image size.
2. Keep images small (Alpine base images).
3. Tag images properly (versioning).
4. Separate configuration from code (environment variables, volumes).

This covers Docker from basics to advanced, including installation, commands, Dockerfile, volumes, networking, compose, registry, and orchestration.





