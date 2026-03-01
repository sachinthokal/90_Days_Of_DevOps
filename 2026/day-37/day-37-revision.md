## Self-Assessment Checklist
Mark yourself honestly — **can do**, **shaky**, or **haven't done**:

- [x] Run a container from Docker Hub (interactive + detached)
- [x] List, stop, remove containers and images
- [x] Explain image layers and how caching works
- [x] Write a Dockerfile from scratch with FROM, RUN, COPY, WORKDIR, CMD
- [x] Explain CMD vs ENTRYPOINT
- [x] Build and tag a custom image
- [x] Create and use named volumes
- [x] Use bind mounts
- [x] Create custom networks and connect containers
- [x] Write a docker-compose.yml for a multi-container app
- [x] Use environment variables and .env files in Compose
- [x] Write a multi-stage Dockerfile
- [x] Push an image to Docker Hub
- [x] Use healthchecks and depends_on

---

## Quick-Fire Questions
```yml
# 🧠 Docker Quick-Fire Q&A

### 1. What is the difference between an image and a container?
* **Image:** A read-only, static template containing the OS, application code, and dependencies. Think of it as the **blueprint** or a "snapshot" of a file system.
* **Container:** A runtime instance of an image. It adds a thin **writable layer** on top of the image.
> **Analogy:** Image = Recipe | Container = The meal being cooked.

### 2. What happens to data inside a container when you remove it?
By default, any data written to the container's internal writable layer is **permanently deleted** when the container is removed (`docker rm`). To persist data, you must use **Volumes** or **Bind Mounts**.

# 3. How do two containers on the same custom network communicate?
They use **DNS resolution via container names**. Docker provides a built-in DNS service for custom networks. If you have a container named `db` and another named `web`, the `web` container can simply reach the database using the hostname `db` instead of an IP address.

### 4. What does `docker compose down -v` do differently?
* `docker compose down`: Stops and removes containers and networks defined in the YAML.
* `-v` (or `--volumes`): Also deletes the **named volumes** declared in the `volumes` section. Use this when you want a "factory reset" of your database/app data.

### 5. Why are multi-stage builds useful?
They allow you to use a heavy image (with compilers/SDKs) to build your app, then **copy only the final artifact** (the binary or minified JS) into a tiny production image (like Alpine). 
* **Benefit:** Resulting images are significantly smaller (e.g., 800MB down to 20MB) and more secure.


### 6. What is the difference between `COPY` and `ADD`?
* **`COPY`:** The standard tool for copying local files/directories into the container. (Use this 99% of the time).
* **`ADD`:** Includes "magic" features: it can fetch files from **remote URLs** and automatically **extract/unpack compressed archives** (.tar, .gzip) during the copy.

### 7. What does `-p 8080:80` mean?
This is **Port Mapping**. It follows the syntax `HOST:CONTAINER`.
* **8080:** The port open on your physical machine/laptop.
* **80:** The port the application is listening on inside the container.
* *Traffic hitting `localhost:8080` is forwarded to port `80` inside the container.*

### 8. How do you check how much disk space Docker is using?
Use the command:
```bash
docker system df
```
---