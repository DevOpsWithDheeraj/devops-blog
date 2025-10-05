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





