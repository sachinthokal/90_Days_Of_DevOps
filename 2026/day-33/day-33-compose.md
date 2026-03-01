# Day 33: Docker Compose - Multi-Container Basics 🐳

Aaj mi shiklo ki kasha prakare `docker-compose.yml` file vaprun complex applications (multi-container) ekach command ne manage karta yetat.

---

## Task 1: Install & Verify
Docker Desktop sobat Compose in-built yete. Linux var aslyas check kara:
```bash
docker compose version
```
### Task 2: Your First Compose File
Folder: compose-basics/
docker-compose.yml:
```yaml
services:
  web-server:
    image: nginx:alpine
    ports:
      - "8080:80"
```
Commands:
- Start: docker compose up -d
- Access: http://localhost:8080
- Stop: docker compose down

### Task 3: Two-Container Setup (WordPress + MySQL)

docker-compose.yml:
```yaml
services:
  db:
    image: mysql:8.0
    volumes:
      - db_data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: somerootpassword
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpresspassword

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpresspassword
      WORDPRESS_DB_NAME: wordpress

volumes:
  db_data:
```

### Task 4: Essential Compose Commands

```bash
Command,Purpose
docker compose up -d # Services background (detached) madhe start karne.
docker compose ps # Running services chi list baghne.
docker compose logs -f # All services madhe logs real-time baghne.
docker compose logs <service> # Specific services che logs real-time baghne.
docker compose logs <service> # Fakt eka specific service che logs baghne.
docker compose stop # Containers stop karne (remove hot nahit).
docker compose down # Containers, Networks ani Images remove karne.
docker compose build # Dockerfile madhle badal reflect karnyathi parat build karne.
```

### Task 5: Environment Variables (.env)
.env File:

DB_PASS=mysecretpassword
WP_PORT=9000

docker-compose.yml (Reference):
```yaml
services:
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_PASS}
  wordpress:
    image: wordpress
    ports:
      - "${WP_PORT}:80"
```

#### Key Learnings
```bash
Service Discovery: # wordpress container db la fakt tyachya navane (DNS) access karu shakto.

Persistence: # volumes mule docker compose down nantar pan data delete hot nahi.

Automation: # Ekach file madhe network, volume ani images che configuration manage hota.
```