# Day 34: Advanced Docker Compose - Production-Like Stacks 🚀

Aaj mi ek 3-tier architecture build kela jyamadhe **Web App**, **Database (Postgres)**, ani **Cache (Redis)** cha samavesh aahe.

---

## Task 1 & 4: The App Stack & Custom Dockerfile
Mi ek sadha Python Flask app banavla jo Redis ani Postgres sobat connect hoto.

**Folder Structure:**
```text
.
├── app/
│   ├── Dockerfile
│   └── app.py
├── docker-compose.yml
└── .env
```
app/Dockerfile:
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install flask redis psycopg2-binary
CMD ["python", "app.py"]
```

### Task 2, 3 & 5: The Advanced docker-compose.yml

docker-compose.yml:
```yaml
services:
  db:
    image: postgres:15-alpine
    container_name: postgres_db
    restart: always
    environment:
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: myapp
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - backend_net
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${DB_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:alpine
    container_name: redis_cache
    restart: on-failure
    networks:
      - backend_net

  web:
    build: ./app
    container_name: flask_app
    ports:
      - "5000:5000"
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started
    networks:
      - frontend_net
      - backend_net
    labels:
      project: "trainwithshubham-day34"

networks:
  frontend_net:
  backend_net:

volumes:
  db_data:

```

### Task 3: Restart Policies (Notes)

Policy | Behavior| Best Use Case | Notes
--- | --- | --- | ---   
always	| Container stop zala ki Docker tyala nehami restart karel.|Critical Databases sathi.|
on-failure	| Fakt jar error mule (exit code non-zero) stop zala tarach restart hoil. |	Scripts kiwa Cron jobs sathi.
unless-stopped |	Manual stop kela asel tar restart honar nahi, baki veli hoil.| Web servers sathi.

### Task 6: Scaling & Port Conflicts (Bonus)
```bash
# docker compose up --scale web=3

Reason: Eka host machine var ek Port (e.g., 5000) fakt ekach container la bind hou shakto. Jar 3 containersna same port pahije asel, tar conflict hoto.
Solution: Production madhe apan Load Balancer (Nginx/HAProxy) vaparto jo bahercha ek port internal containers chya dynamic ports la map karto
```