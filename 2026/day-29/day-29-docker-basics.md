# Day 29: Docker Fundamentals & Container Basics

## Task 1: Understanding Docker

### 1. What is a container and why do we need them?
A container is a lightweight, standalone, executable package that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings. 

**Why we need them:** They solve the "It works on my machine" problem. By packaging the environment with the code, applications run identically across development, testing, and production environments, regardless of the underlying host OS.

### 2. Containers vs. Virtual Machines (VMs)
* **Virtual Machines:** Each VM includes a full copy of an operating system, the application, and necessary binaries. They run on top of a Hypervisor and are resource-heavy (GBs in size).
* **Containers:** Containers share the host system's OS kernel. They do not require a guest OS, making them extremely lightweight (MBs in size), fast to boot, and highly efficient.



### 3. Docker Architecture
The Docker architecture follows a client-server model:
* **Docker Client:** The primary way users interact with Docker. When you run `docker run`, the client sends the command to the daemon.
* **Docker Daemon (dockerd):** The brain of Docker. It listens for API requests and manages Docker objects like images, containers, networks, and volumes.
* **Images:** Read-only templates used to create containers.
* **Containers:** The live, running instances of images.
* **Registry:** A place to store and share images (e.g., Docker Hub).



---

## Task 3 & 4: Docker Hands-On Guide

### Basic Management Commands
| Command | Action |
| :--- | :--- |
| `docker run` | Pulls an image (if not local), creates a container, and starts it. |
| `docker ps` | Lists all **running** containers. |
| `docker ps -a` | Lists **all** containers, including those that have exited. |
| `docker stop <ID>` | Gracefully stops a running container. |
| `docker rm <ID>` | Permanently removes a stopped container. |
| `docker rmi <Image>` | Removes a downloaded image from your local machine. |

### Advanced Execution Flags
* **Detached Mode (`-d`)**: Runs the container in the background, allowing you to keep using your terminal.
* **Interactive Mode (`-it`)**: Connects your terminal to the container's shell (useful for Ubuntu/Alpine containers).
* **Port Mapping (`-p host:container`)**: Forwards traffic from your machine to the container (e.g., `-p 8080:80`).
* **Naming (`--name`)**: Assigns a custom name to the container for easier management.

---

## Observations from Tasks

### Running Nginx
Command: `docker run -d --name web-server -p 8080:80 nginx`
* **Observation:** After running this, I could visit `localhost:8080` in my browser and see the "Welcome to nginx!" page. The container stayed running in the background due to the `-d` flag.

### Ubuntu Interactive Session
Command: `docker run -it ubuntu bash`
* **Observation:** My terminal prompt changed. I was now `root` inside a minimal Linux environment. I could run `apt update` or explore the file system, but these changes vanish if the container is removed.

### Viewing Logs & Executing Commands
* **Logs:** `docker logs web-server` allowed me to see the HTTP request history.
* **Exec:** `docker exec -it web-server ls /etc/nginx` allowed me to look at the configuration files without stopping the running servers.