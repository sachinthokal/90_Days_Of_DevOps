# Day 31: Dockerfile - Build Your Own Images

Hi mazi Day 31 chi practice file aahe, jyamadhe mi custom Docker images build karayla shiklo.

---

## Task 1: Your First Dockerfile
**Folder:** `my-first-image/`

**Dockerfile:**
```dockerfile
# 1. FROM: Base image foundation
FROM python:3.9-slim

# 2. WORKDIR: Set the working directory
WORKDIR /app

# 3. COPY: Copy local files into the container
COPY . .

# 4. RUN: Execute commands during build (Install Flask)
RUN pip install --no-cache-dir flask

# 5. EXPOSE: Inform which port the app runs on
EXPOSE 5000

# 6. CMD: Final command to start the application
CMD ["python", "app.py"]
```
### Task 3: CMD vs ENTRYPOINT
```bash

CMD: # He override karta yete. docker run image <command> dile ki CMD skip hoto.

ENTRYPOINT: # He fixed aste. Run time la dilele arguments hya executable la attach hotat.

# Notes: - CMD tabha vapra jayvha tumhala default arguments dyayche astil.

ENTRYPOINT # tevha vapra jayvha tumhala container la ek 'executable tool' banvayche asel

```
### Task 4: Simple Web App (Nginx)
```bash
# index.html:

<!DOCTYPE html>
<html>
<head><title>Day 31 Task</title></head>
<body>
    <h1>Welcome to Day 31 of 90 Days of DevOps!</h1>
    <p>Custom Nginx Image successfully built and running.</p>
</body>
</html>

# Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html

# Commands
docker build -t my-website:v1 .
docker run -d -p 8080:80 my-website:v1
```
### Task 5: .dockerignore
```bash
node_modules
.git
*.md
.env

```

### Task 6: Build Optimization (Layer Caching)
```bash

Docker madhe pratyek instruction ek Layer tyaar karte.

# Key Learnings:

Docker cache vaprun build fast karte.

Order matters: Ja goshti kamit-kami badaltat (like OS updates), tya varati (top) theva.

Code COPY: COPY . . nehami shevti (bottom) theva, karan code warun-warun change hoto.

```