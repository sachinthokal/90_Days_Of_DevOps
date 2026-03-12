## Complete CI/CD pipeline for Joke-App
```yml
name: JOKE APP CICD

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to Docker Hub
        if: github.event_name != 'pull_request' && github.ref == 'refs/heads/main'
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_TOKEN }}

      - name: Extract Metadata (Short SHA)
        id: vars
        run: echo "sha_short=$(git rev-parse --short HEAD)" >> $GITHUB_OUTPUT

      - name: Build and Push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: ${{ github.event_name != 'pull_request' && github.ref == 'refs/heads/main' }}
          tags: |
            ${{ secrets.DOCKER_USERNAME }}/joke_app:latest
            ${{ secrets.DOCKER_USERNAME }}/joke_app:sha-${{ steps.vars.outputs.sha_short }}

```
---
![alt text](image-1.png)
### Live Site via Github Actions CICD
![alt text](image.png)