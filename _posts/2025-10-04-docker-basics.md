---
layout: post
title: "Docker Basics for DevOps"
date: 2025-10-04
---

# Docker Basics for DevOps

Docker is a powerful **containerization platform** that allows developers and DevOps engineers to **build, ship, and run applications in isolated environments** called containers. Containers are lightweight, portable, and consistent across different environments — making them ideal for DevOps workflows.

In this post, we will cover **everything from Docker basics to advanced concepts**, including commands, examples, and best practices.

---

## 1. Why Docker?

Traditional deployment often leads to issues like **“it works on my machine but not on production”**. Docker solves this problem by:

- Packaging **applications with all dependencies** in a container.
- Ensuring **environment consistency** across dev, test, and prod.
- Reducing resource usage compared to virtual machines (VMs).
- Enabling **faster CI/CD pipelines**.

---

## 2. Container vs Virtual Machine

| Feature               | Container                   | Virtual Machine         |
|-----------------------|----------------------------|------------------------|
| Resource usage        | Lightweight                | Heavy                  |
| Startup time          | Seconds                     | Minutes                |
| Isolation             | Process-level               | Hardware-level         |
| OS Requirement        | Shares host OS              | Full OS per VM         |
| Portability           | Very high                   | Moderate               |

**Key takeaway:** Containers share the host OS kernel, making them faster and more efficient.

---

## 3. Docker Architecture

- **Docker Engine:** Core service to build and run containers.
- **Docker Image:** Blueprint for a container (read-only).
- **Docker Container:** Running instance of an image.
- **Docker Hub:** Public registry to share images.
- **Docker Compose:** Tool to define and manage multi-container applications.

---

## 4. Installing Docker

### On Ubuntu

sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker       # Start Docker service
sudo systemctl enable docker      # Enable Docker on boot
docker --version                  # Check installed Docker version

