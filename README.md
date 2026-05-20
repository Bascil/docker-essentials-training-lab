# docker-essentials-training-lab

## Introduction

This hands-on training introduces the **fundamentals of Docker**, focusing on installation, image management, container lifecycle, and basic database container interaction. Docker is a containerization platform that enables developers to package applications and their dependencies into lightweight, portable containers that run consistently across environments.

---

## Objective

The objective of this lab is to provide learners with practical experience in:

- Installing and configuring Docker on a Linux system
- Pulling and managing container images from Docker Hub
- Running and exposing services using containers
- Interacting with running containers
- Managing container lifecycle (start, stop, logs, remove)
- 
---

# Lab 1: Install Docker

## Install Docker on Ubuntu/Debian

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker
```

## Add User to Docker Group

```bash
sudo usermod -aG docker $USER
newgrp docker
```

## Verify Installation

```bash
docker --version
```

---

# Lab 2: Docker Images & Containers

## Nginx Web Server

**Pull image**

```bash
docker pull nginx
```

**Run container**

```bash
docker run -d -p 8080:80 nginx
```

**Access**

```
http://localhost:8080
```

---

## MySQL Container Lab

**Pull image**

```bash
docker pull mysql:8
```

**Run container**

```bash
docker run -d \
  --name mysql-lab \
  -e MYSQL_ROOT_PASSWORD=MyStrongPass123 \
  -p 3307:3306 \
  mysql:8
```

**Check running containers**

```bash
docker ps
```

**Access MySQL container**

```bash
docker exec -it mysql-lab mysql -u root -p
```

**Inside MySQL**

```sql
CREATE DATABASE dockerlab;
USE dockerlab;
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100)
);
INSERT INTO users(name) VALUES ('Docker User');
```

---

## Logs

```bash
docker logs mysql-lab
```

## Stop & Remove

```bash
docker stop mysql-lab
docker rm mysql-lab
```

---

## Summary

This lab demonstrated how Docker simplifies application deployment using containers. You learned installation, image management, running services, and interacting with containerized applications.
