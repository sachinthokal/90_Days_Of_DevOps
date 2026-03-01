# Day 35: Multi-Stage Builds & Docker Hub 🚀

Aaj mi Docker imagesna optimize karayla ani jagasobat share karayla (Docker Hub var) shiklo. Multi-stage build mhanje Docker madhli ek powerful technique aahe jya mule image size 90% paryant kami hou shakto.

---

## Task 1 & 2: The Magic of Multi-Stage Builds

Mi ek Go (Golang) cha app vaparla karan Go madhe compilation nantar ek single binary tyaar hote.

### 1. Single-Stage Build (The Heavy Way)
Hya image madhe build tools ani source code saglach rahte.
**Dockerfile.heavy:**
```dockerfile
FROM golang:1.21
WORKDIR /app
COPY . .
RUN go build -o main .
CMD ["./main"]

Size: ~800MB - 900MB

2. Multi-Stage Build (The DevOps Way)
Dockerfile:

# Stage 1: Build Stage
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp .

# Stage 2: Final Run Stage
FROM alpine:latest
# Security: Add non-root user
RUN adduser -D devopsuser
USER devopsuser
WORKDIR /app
# Only copy the binary from the builder stage
COPY --from=builder /app/myapp .
CMD ["./myapp"]

Size: ~15MB - 20MB 😍

Why is it smaller? Final image madhe Go compiler, cache, ani source code nasto. Fakt tya app la lagmari binary ani ek choti Alpine OS chi layer aste.
```
### Task 3 & 4: Pushing to Docker Hub 🌎

Mazi image mi Docker Hub var push keli.
```bash
Steps:

Login: docker login -u yourusername
Tag: docker tag go-app:v1 yourusername/go-app:v1
Push: docker push yourusername/go-app:v1
My Repository Link: https://hub.docker.com/r/yourusername/go-app
```

### Task 5: Docker Image Best Practices (Checklist)

Practice |	Why? |
--- | --- |
Minimal Base Image |	alpine vaparlyane security vulnerabilities kami hotat ani size sudha.
Non-Root User |	Container jar hack zale, tar attacker la root access milat nahi.
Layer Reduction	 |RUN apt update && apt install -y ... ashi commands combine kelyane layers kami hotat.
Specific Tags |	python:3.9-slim vapra, latest nako. Karan latest tag kadhi pan badlu shakto.

---

Comparison Table: Before vs After

Metric	| Single-Stage |	Multi-Stage (Optimized) |
--- | --- | --- |
Base Image |	golang:1.21 | alpine:latest |
Image Size |	850 MB |	18 MB
Security |	Low (Full OS tools)|	High (Minimal tools + Non-root)
Build Time |	Slow?	| Fast (due to caching)

---