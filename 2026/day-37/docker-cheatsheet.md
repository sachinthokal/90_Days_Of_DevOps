# 🐳 Docker CLI Cheat Sheet

A comprehensive guide to the most common Docker commands and workflows.

---

## 🏗️ Images
Build, manage, and remove images.

| Command | Description |
| :--- | :--- |
| `docker build -t <name> .` | Build an image from a Dockerfile in the current directory |
| `docker images` | List all locally stored images |
| `docker rmi <image_id>` | Remove a specific image |
| `docker tag <src> <target>` | Create a tag (alias) for an image |
| `docker pull <image>` | Download an image from Docker Hub |
| `docker push <image>` | Upload an image to a registry |
| `docker image prune` | Remove all unused images |

---

## 🚀 Containers
Managing the lifecycle of your containers.

| Command | Description |
| :--- | :--- |
| `docker run -d --name <name> <image>` | Run container in background (detached) |
| `docker run -it <image> /bin/bash` | Run container and enter its interactive shell |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (including stopped ones) |
| `docker stop <container>` | Stop a running container |
| `docker start <container>` | Start a stopped container |
| `docker rm <container>` | Remove a container |
| `docker rm -f $(docker ps -aq)` | **Nuclear option:** Remove ALL containers |

---

## 🔍 Inspection & Logs
Debugging what's happening inside.

* **View logs:** `docker logs -f <container>` (The `-f` follows live output).
* **Inspect metadata:** `docker inspect <container_id>` (Returns JSON details).
* **Real-time stats:** `docker stats` (CPU, Memory, Network usage).
* **Check ports:** `docker port <container>` (See mapped ports).
* **Execute command:** `docker exec -it <container> <command>` (Run a command in a running container).

---

## 💾 Volumes & Networking
Persisting data and connecting containers.



* **Create a volume:** `docker volume create <name>`
* **List volumes:** `docker volume ls`
* **Run with volume:** `docker run -v <volume_name>:/data <image>`
* **Create network:** `docker network create <name>`
* **Connect container:** `docker network connect <network> <container>`

---

## 🐙 Docker Compose
Managing multi-container applications.

* `docker-compose up -d` : Start all services in the background.
* `docker-compose down` : Stop and remove containers, networks, and images.
* `docker-compose logs -f` : View logs for all services.
* `docker-compose ps` : List status of services.
* `docker-compose build` : Rebuild services defined in the YAML file.

---

## 🧹 Cleanup
Keep your system lean.

> **Warning:** These commands remove data. Use with caution!

* **Prune everything:** `docker system prune` (Removes stopped containers, unused networks, and dangling images).
* **Deep clean:** `docker system prune -a --volumes` (Includes unused images and all volumes).