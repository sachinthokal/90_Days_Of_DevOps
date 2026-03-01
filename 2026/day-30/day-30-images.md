# Task 1: Docker Images

## Pull Images

``` bash
docker pull nginx
docker pull ubuntu
docker pull alpine
```
## List Images

``` bash
docker images
```
### Ubuntu vs Alpine

-   Ubuntu is large (\~70MB+) because it includes full OS utilities.
-   Alpine is very small (\~5MB) because it is minimal and uses musl
    libc.

## Inspect Image

``` bash
docker inspect nginx
```

Information available: - Image ID - Layers - Environment variables -
Entrypoint - Default command - Architecture

## Remove Image

``` bash
docker rmi ubuntu
```

------------------------------------------------------------------------

# Task 2: Image Layers

## View Image History

``` bash
docker image history nginx
```

### What are Layers?

-   Each instruction in a Dockerfile creates a layer.
-   Layers are cached to speed up builds.
-   Shared layers reduce storage usage.
-   0B layers usually represent metadata changes.

Docker uses layers for: - Efficient storage - Faster builds -
Reusability across images

------------------------------------------------------------------------

# Task 3: Container Lifecycle

## Create (without start)

``` bash
docker create --name mynginx nginx
```

## Start

``` bash
docker start mynginx
```

## Pause

``` bash
docker pause mynginx
docker ps
```

## Unpause

``` bash
docker unpause mynginx
```

## Stop

``` bash
docker stop mynginx
```

## Restart

``` bash
docker restart mynginx
```

## Kill

``` bash
docker kill mynginx
```

## Remove

``` bash
docker rm mynginx
```

States Observed: - Created - Running - Paused - Exited

------------------------------------------------------------------------

# Task 4: Working with Running Containers

## Run Nginx in Detached Mode

``` bash
docker run -d -p 8080:80 --name web nginx
```

## View Logs

``` bash
docker logs web
```

## Follow Logs (Real-time)

``` bash
docker logs -f web
```

## Exec into Container

``` bash
docker exec -it web /bin/bash
```

## Run Single Command

``` bash
docker exec web ls /usr/share/nginx/html
```

## Inspect Container

``` bash
docker inspect web
```

Find: - IP Address - Port Bindings - Mounts - Network settings

------------------------------------------------------------------------

# Task 5: Cleanup

## Stop All Running Containers

``` bash
docker stop $(docker ps -q)
```

## Remove All Stopped Containers

``` bash
docker rm $(docker ps -aq)
```

## Remove Unused Images

``` bash
docker image prune -a
```

## Check Disk Usage

``` bash
docker system df
```
------------------------------------------------------------------------

# Key Learnings

-   Images are blueprints; containers are running instances.
-   Layers make Docker efficient and fast.
-   Containers move through defined lifecycle states.
-   Alpine is preferred in production for smaller attack surface.
-   Proper cleanup prevents disk space issues.

------------------------------------------------------------------------
