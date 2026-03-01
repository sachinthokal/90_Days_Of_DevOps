# Day 32: Docker Volumes & Networking 🚀

Aaj mi Docker madhle don sarvat mahatvache concepts shiklo: **Data Persistence** (Volumes) ani **Container Communication** (Networking).

---

## Task 1: The Problem (Ephemeral Nature)
Mi ek Postgres container run kela ani tyat dummy data takla.
```bash
docker run --name my-db -e POSTGRES_PASSWORD=password -d postgres
docker exec -it my-db psql -U postgres -c "CREATE TABLE test (id serial PRIMARY KEY, name VARCHAR(50));"
docker stop my-db && docker rm my-db

# Observation: Jayvha mi navin container run kela, tavha maza test table gayab zala hota.
# Why? Containers 'Ephemeral' astat. Container delete kela ki tyatla data pan delete hoto.
```
### Task 2: Named Volumes (Solution)
```bash
# 1. Volume create kara
docker volume create pg-data

# 2. Volume attach karun container run kara
docker run --name my-stable-db -v pg-data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=password -d postgres

# 3. Data taka, container delete kara ani parat run kara
docker rm -f my-stable-db
docker run --name my-stable-db-v2 -v pg-data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=password -d postgres

```

### Task 3: Bind Mounts (Solution)
```bash
# Bind mount madhe host machine varchi folder container la share kartat.

# Steps:

# Folder banavli: mkdir my-site && echo "<h1>Hello from Host</h1>" > my-site/index.html

# Run Nginx: docker run -d -p 8080:80 -v $(pwd)/my-site:/usr/share/nginx/html nginx:alpine

# Named Volume vs Bind Mount:
```
| Feature | Named Volume | Bind Mount |
| :--- | :--- | :--- |
| Storage | Docker manage karto (/var/lib/docker/volumes) | Tu tharavleli folder (Host path) |
| Usage | Databases sathi best | Source code sharing sathi best |

```
```
### Task 4 & 5: Docker Networking
```bash

# Default Bridge vs Custom Network:

# Default Bridge: Containersna ekmekanla ping karnyathi IP Address lagto. Container name ne ping hot nahi.

# Custom Network: Hyat Automatic Service Discovery aste. Tu container chya naavane (Name) ping karu shakto.

# Commands for Custom Network:

# docker network create my-app-net
# docker run -d --name db --network my-app-net postgres
# docker run -d --name web --network my-app-net nginx
# docker exec -it web ping db

```
### Task 6: Put It Together (Full Setup)

```bash
# 1. Network & Volume
docker network create final-net
docker volume create db-storage

# 2. Run Database
docker run -d --name database --network final-net -v db-storage:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest

# 3. Run App (Alpine for testing)
docker run -it --name app-server --network final-net alpine sh
# Inside app-server: ping database (It works!)

```