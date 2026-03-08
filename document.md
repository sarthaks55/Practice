Great that you’re starting **DevOps with Docker** 🚀. These commands are the **core daily commands** every DevOps engineer uses. I’ll explain them in a **simple + practical way** with:

* What the command does
* Basic syntax
* Example
* When it is used in real DevOps work

---

# 1. `docker version`

### What it does

Shows the **Docker client and server version** installed on your machine.

### Syntax

```bash
docker version
```

### Example

```bash
docker version
```

### Output shows

* Client version
* Server version
* API version
* Go version

### When used

To verify Docker installation.

---

# 2. `docker search`

### What it does

Searches images from **Docker Hub registry**.

### Syntax

```bash
docker search <image_name>
```

### Example

```bash
docker search nginx
```

### Output

Shows:

* image name
* description
* stars
* official image

Example result:

```
nginx        Official build of Nginx
nginx-unit   Official Nginx Unit image
```

### When used

When you want to **find available images**.

---

# 3. `docker pull`

### What it does

Downloads an **image from Docker Hub** to your local system.

### Syntax

```bash
docker pull <image_name>
```

### Example

```bash
docker pull nginx
```

Specific version:

```bash
docker pull nginx:1.25
```

### When used

Before running a container.

---

# 4. `docker run`

### What it does

Creates **and starts a container** from an image.

### Syntax

```bash
docker run [options] <image>
```

### Example

```bash
docker run nginx
```

Run in background:

```bash
docker run -d nginx
```

Run with port mapping:

```bash
docker run -d -p 8080:80 nginx
```

### Common options

| Option | Meaning              |
| ------ | -------------------- |
| -d     | detached mode        |
| -p     | port mapping         |
| -it    | interactive terminal |
| --name | container name       |

Example

```bash
docker run -it ubuntu bash
```

---

# 5. `docker ps`

### What it does

Shows **running containers**.

### Syntax

```bash
docker ps
```

### Example output

```
CONTAINER ID   IMAGE   STATUS
abc123         nginx   Up 5 minutes
```

---

# 6. `docker ps -a`

### What it does

Shows **all containers** (running + stopped).

### Syntax

```bash
docker ps -a
```

---

# 7. `docker stop`

### What it does

Stops a running container **gracefully**.

### Syntax

```bash
docker stop <container_id>
```

### Example

```bash
docker stop abc123
```

---

# 8. `docker restart`

### What it does

Stops and starts the container again.

### Syntax

```bash
docker restart <container_id>
```

Example

```bash
docker restart nginx_container
```

---

# 9. `docker kill`

### What it does

Forcefully stops a container.

### Syntax

```bash
docker kill <container_id>
```

### Difference

| stop          | kill           |
| ------------- | -------------- |
| Graceful stop | Immediate stop |

---

# 10. `docker exec`

### What it does

Runs a command **inside a running container**.

### Syntax

```bash
docker exec [options] <container> <command>
```

### Example

Access container shell

```bash
docker exec -it nginx_container bash
```

Check files

```bash
docker exec nginx_container ls
```

---

# 11. `docker login`

### What it does

Login to **Docker Hub registry**.

### Syntax

```bash
docker login
```

You will enter:

```
username
password
```

---

# 12. `docker logout`

### What it does

Logs out of Docker registry.

### Syntax

```bash
docker logout
```

---

# 13. `docker commit`

### What it does

Creates a **new image from a container**.

### Syntax

```bash
docker commit <container_id> <new_image_name>
```

### Example

```bash
docker commit abc123 my-nginx
```

### When used

When you modify a container and want to **save it as an image**.

---

# 14. `docker push`

### What it does

Uploads an image to **Docker Hub**.

### Syntax

```bash
docker push <username>/<image>
```

### Example

```bash
docker push mydockeruser/my-nginx
```

Steps normally:

```
docker build
docker tag
docker push
```

---

# 15. `docker network`

### What it does

Manages Docker networks.

### Syntax

```bash
docker network <command>
```

### Common commands

Create network

```bash
docker network create mynetwork
```

List networks

```bash
docker network ls
```

Inspect network

```bash
docker network inspect mynetwork
```

Used for **container communication**.

---

# 16. `docker history`

### What it does

Shows **layers used to build an image**.

### Syntax

```bash
docker history <image>
```

Example

```bash
docker history nginx
```

Shows:

* layers
* size
* commands used

---

# 17. `docker rmi`

### What it does

Deletes an image.

### Syntax

```bash
docker rmi <image_id>
```

Example

```bash
docker rmi nginx
```

Force remove

```bash
docker rmi -f nginx
```

---

# 18. `docker cp`

### What it does

Copies files **between host and container**.

### Syntax

```bash
docker cp <source> <container>:<destination>
```

### Example

Host → Container

```bash
docker cp file.txt container_id:/app
```

Container → Host

```bash
docker cp container_id:/app/file.txt .
```

---

# 19. `docker logs`

### What it does

Shows container logs.

### Syntax

```bash
docker logs <container>
```

### Example

```bash
docker logs nginx_container
```

Live logs

```bash
docker logs -f nginx_container
```

---

# 20. `docker volume`

### What it does

Manages **persistent storage**.

Containers normally lose data when deleted.
Volumes keep data safe.

### Syntax

```bash
docker volume <command>
```

### Common commands

Create volume

```bash
docker volume create myvolume
```

List volumes

```bash
docker volume ls
```

Inspect volume

```bash
docker volume inspect myvolume
```

Use volume

```bash
docker run -v myvolume:/data nginx
```

---

# Real DevOps Workflow Example

Typical workflow:

1️⃣ Pull image

```bash
docker pull nginx
```

2️⃣ Run container

```bash
docker run -d -p 80:80 nginx
```

3️⃣ Check container

```bash
docker ps
```

4️⃣ See logs

```bash
docker logs container_id
```

5️⃣ Access container

```bash
docker exec -it container_id bash
```

6️⃣ Stop container

```bash
docker stop container_id
```

---

# Docker Concepts You Should Also Know

Since you're learning DevOps, understand these too:

* Docker Images
* Docker Containers
* Dockerfile
* Docker Compose
* Docker Volumes
* Docker Networking
* Docker Registry

These are **essential for DevOps interviews**.

---




Good question 👍. In real DevOps work, engineers **don’t use every Docker command daily**. Usually **20–25 commands cover almost 90% of real work**. I’ll show you the **most commonly used commands in real projects**, grouped by purpose.

---

# 1️⃣ Docker Environment & Information Commands

These are used to **check Docker installation and system status**.

### Check Docker version

```bash
docker version
```

### Show Docker system information

```bash
docker info
```

Shows:

* number of containers
* images
* storage driver
* CPU / memory

### Check Docker disk usage

```bash
docker system df
```

---

# 2️⃣ Image Management Commands

DevOps engineers constantly **download, build, tag, and push images**.

### Pull image from Docker Hub

```bash
docker pull nginx
```

### List images

```bash
docker images
```

### Remove image

```bash
docker rmi nginx
```

Force remove:

```bash
docker rmi -f nginx
```

### Build image from Dockerfile

```bash
docker build -t myapp .
```

### Tag image

```bash
docker tag myapp username/myapp:v1
```

### Push image to Docker Hub

```bash
docker push username/myapp:v1
```

---

# 3️⃣ Container Management Commands

These are **the most used commands daily**.

### Run container

```bash
docker run nginx
```

Run in background:

```bash
docker run -d nginx
```

Run with port mapping:

```bash
docker run -d -p 8080:80 nginx
```

Run with container name:

```bash
docker run -d --name web nginx
```

---

### List running containers

```bash
docker ps
```

### List all containers

```bash
docker ps -a
```

---

### Stop container

```bash
docker stop container_id
```

### Start container

```bash
docker start container_id
```

### Restart container

```bash
docker restart container_id
```

### Kill container

```bash
docker kill container_id
```

---

### Remove container

```bash
docker rm container_id
```

Force remove:

```bash
docker rm -f container_id
```

---

# 4️⃣ Debugging Containers (Very Important)

DevOps engineers spend **a lot of time debugging containers**.

### Check container logs

```bash
docker logs container_id
```

Live logs:

```bash
docker logs -f container_id
```

---

### Enter container shell

```bash
docker exec -it container_id bash
```

or

```bash
docker exec -it container_id sh
```

Used for:

* debugging
* checking files
* checking processes

---

### Inspect container details

```bash
docker inspect container_id
```

Shows:

* IP address
* mounts
* networks
* environment variables

---

# 5️⃣ File Copy Commands

Sometimes you need to **move files between container and host**.

### Copy host → container

```bash
docker cp file.txt container_id:/app
```

### Copy container → host

```bash
docker cp container_id:/app/file.txt .
```

---

# 6️⃣ Docker Volume Commands

Used to **store persistent data**.

### List volumes

```bash
docker volume ls
```

### Create volume

```bash
docker volume create myvolume
```

### Inspect volume

```bash
docker volume inspect myvolume
```

### Remove volume

```bash
docker volume rm myvolume
```

Example run with volume:

```bash
docker run -v myvolume:/data nginx
```

---

# 7️⃣ Docker Network Commands

Used for **container communication**.

### List networks

```bash
docker network ls
```

### Create network

```bash
docker network create mynetwork
```

### Inspect network

```bash
docker network inspect mynetwork
```

### Connect container to network

```bash
docker network connect mynetwork container_id
```

---

# 8️⃣ Docker Cleanup Commands (Very Important)

Docker quickly fills disk space. DevOps engineers regularly clean it.

### Remove stopped containers

```bash
docker container prune
```

### Remove unused images

```bash
docker image prune
```

### Remove everything unused

```bash
docker system prune
```

Remove everything including volumes:

```bash
docker system prune -a
```

---

# 9️⃣ Docker Login & Registry Commands

Used when working with **Docker Hub or private registries**.

### Login

```bash
docker login
```

### Logout

```bash
docker logout
```

---

# 🔟 Example Real DevOps Workflow

Typical workflow used daily:

### 1 Pull image

```bash
docker pull node:18
```

### 2 Build application image

```bash
docker build -t myapp .
```

### 3 Run container

```bash
docker run -d -p 3000:3000 myapp
```

### 4 Check running containers

```bash
docker ps
```

### 5 Check logs

```bash
docker logs -f container_id
```

### 6 Enter container for debugging

```bash
docker exec -it container_id bash
```

### 7 Push image to Docker Hub

```bash
docker tag myapp username/myapp:v1
docker push username/myapp:v1
```

---

# ⭐ Top 15 Docker Commands Used Daily (Remember These)

These are **most important for DevOps interviews**.

```
docker build
docker run
docker ps
docker ps -a
docker stop
docker start
docker restart
docker rm
docker rmi
docker logs
docker exec
docker images
docker pull
docker push
docker system prune
```

---

---



Learning **Dockerfile** is the next important step after basic Docker commands. A **Dockerfile lets you create your own custom Docker images**, which is something DevOps engineers do very often in real projects. Let’s go step-by-step. 🚀

---

# 1️⃣ What is a Dockerfile?

A **Dockerfile** is a **text file that contains instructions to build a Docker image automatically**.

Instead of manually configuring a container and using `docker commit`, you define everything in code.

Think of it like:

```
Dockerfile = Recipe
Image = Prepared food
Container = Running food order
```

---

# 2️⃣ Basic Dockerfile Structure

Example Dockerfile:

```dockerfile
# Base image
FROM ubuntu:22.04

# Install packages
RUN apt-get update && apt-get install -y nginx

# Copy files
COPY . /app

# Set working directory
WORKDIR /app

# Expose port
EXPOSE 80

# Start application
CMD ["nginx", "-g", "daemon off;"]
```

This builds an image that runs **NGINX inside Ubuntu**.

---

# 3️⃣ Important Dockerfile Instructions

## 1️⃣ `FROM`

Defines the **base image**.

Every Dockerfile must start with it.

```dockerfile
FROM ubuntu:22.04
```

Examples:

```dockerfile
FROM node:18
FROM python:3.10
FROM nginx
FROM alpine
```

Why needed:

* You don’t start from scratch
* You reuse existing OS or runtime

---

## 2️⃣ `RUN`

Executes commands during **image build time**.

Example:

```dockerfile
RUN apt-get update
RUN apt-get install -y nginx
```

Better practice (single layer):

```dockerfile
RUN apt-get update && apt-get install -y nginx
```

Used for:

* Installing packages
* Creating directories
* Downloading dependencies

Example:

```dockerfile
RUN mkdir /app
```

---

## 3️⃣ `COPY`

Copies files from **host → container image**.

```dockerfile
COPY <source> <destination>
```

Example:

```dockerfile
COPY index.html /usr/share/nginx/html/
```

Copy everything:

```dockerfile
COPY . .
```

---

## 4️⃣ `ADD` (Similar to COPY)

```dockerfile
ADD file.txt /app/
```

Difference:

* `ADD` can extract **compressed files**
* `COPY` is simpler and preferred

Most DevOps engineers prefer **COPY**.

---

## 5️⃣ `WORKDIR`

Sets the working directory inside container.

```dockerfile
WORKDIR /app
```

Now every command runs inside `/app`.

Example:

```dockerfile
WORKDIR /app
COPY . .
RUN npm install
```

---

## 6️⃣ `EXPOSE`

Documents the port used by the container.

```dockerfile
EXPOSE 80
```

Important:
It **does NOT publish the port**, it only documents it.

You still run:

```bash
docker run -p 8080:80 image
```

---

## 7️⃣ `ENV`

Sets environment variables.

```dockerfile
ENV APP_ENV=production
```

Example:

```dockerfile
ENV NODE_ENV=production
```

---

## 8️⃣ `CMD`

Defines the **default command** when container starts.

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

Only **one CMD should exist**.

If multiple CMD exist → last one runs.

---

## 9️⃣ `ENTRYPOINT`

Similar to CMD but **cannot be overridden easily**.

Example:

```dockerfile
ENTRYPOINT ["python"]
```

Then:

```bash
docker run myimage app.py
```

Runs:

```
python app.py
```

---

# 4️⃣ Step-by-Step: Create Your First Dockerfile

Let's build a **simple Nginx website container**.

---

## Step 1: Create project folder

```bash
mkdir docker-nginx
cd docker-nginx
```

---

## Step 2: Create HTML file

Create `index.html`

```html
<h1>Hello from my Docker container 🚀</h1>
```

---

## Step 3: Create Dockerfile

Create file named **Dockerfile**

(no extension)

```
Dockerfile
```

Content:

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

---

## Step 4: Build Image

```bash
docker build -t my-nginx .
```

Explanation:

| Part         | Meaning           |
| ------------ | ----------------- |
| docker build | build image       |
| -t           | tag image         |
| my-nginx     | image name        |
| .            | current directory |

---

## Step 5: Run Container

```bash
docker run -d -p 8080:80 my-nginx
```

Open browser:

```
http://localhost:8080
```

You will see:

```
Hello from my Docker container 🚀
```

---

# 5️⃣ Example: Node.js Dockerfile

A real DevOps example.

Project structure:

```
app/
 ├── package.json
 ├── server.js
 └── Dockerfile
```

Dockerfile:

```dockerfile
FROM node:18

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

Build:

```bash
docker build -t my-node-app .
```

Run:

```bash
docker run -p 3000:3000 my-node-app
```

---

# 6️⃣ How Docker Builds Images (Layers)

Every Dockerfile instruction creates a **layer**.

Example:

```
FROM ubuntu
RUN apt install nginx
COPY index.html
```

Layers:

```
Layer 1 → ubuntu base
Layer 2 → install nginx
Layer 3 → copy file
```

Why important:

* Faster builds
* Cached layers
* Smaller changes

---

# 7️⃣ Dockerfile Best Practices (Important for DevOps)

### 1️⃣ Use small base images

Bad

```
FROM ubuntu
```

Better

```
FROM alpine
```

---

### 2️⃣ Combine RUN commands

Bad

```dockerfile
RUN apt update
RUN apt install nginx
```

Good

```dockerfile
RUN apt update && apt install -y nginx
```

---

### 3️⃣ Use `.dockerignore`

Like `.gitignore`.

Example:

```
node_modules
.git
logs
```

Prevents unnecessary files in image.

---

### 4️⃣ Use specific image versions

Bad

```
FROM node:latest
```

Good

```
FROM node:18
```

---

# 8️⃣ Real DevOps Workflow with Dockerfile

Typical CI/CD process:

```
Developer pushes code
        ↓
CI tool (Jenkins/GitHub Actions)
        ↓
Docker build
        ↓
Docker image created
        ↓
Push to Docker Hub
        ↓
Deploy to Kubernetes
```

Commands used:

```
docker build
docker tag
docker push
```

---

# 9️⃣ Commands Used with Dockerfile

Build image

```bash
docker build -t myapp .
```

List images

```bash
docker images
```

Run container

```bash
docker run myapp
```

---

# 🔟 Example Real Production Dockerfile

Example for **Python app**.

```dockerfile
FROM python:3.10

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

---




A **real DevOps Docker workflow** shows how code moves from a developer’s laptop → Docker image → CI/CD → production deployment. Understanding this flow will help you see **where Docker fits in the DevOps pipeline**. 🚀

---

# 1️⃣ High-Level DevOps Docker Workflow

Typical pipeline used in companies:

```
Developer writes code
        ↓
Push to Git repository (GitHub / GitLab)
        ↓
CI/CD pipeline starts (Jenkins / GitHub Actions)
        ↓
Build Docker image
        ↓
Run tests inside container
        ↓
Push image to Docker Registry
        ↓
Deploy container to server / Kubernetes
```

Docker is mainly used in the **build and deployment stages**.

---

# 2️⃣ Step 1: Developer Writes Application

Example: A simple **Node.js app**.

Project structure:

```
my-app/
 ├── app.js
 ├── package.json
 └── Dockerfile
```

Example `app.js`

```javascript
const express = require("express")
const app = express()

app.get("/", (req,res)=>{
res.send("Hello from Docker DevOps workflow 🚀")
})

app.listen(3000)
```

---

# 3️⃣ Step 2: Create Dockerfile

DevOps engineers containerize the application.

Example Dockerfile:

```dockerfile
FROM node:18

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node","app.js"]
```

What happens:

| Step    | Description             |
| ------- | ----------------------- |
| FROM    | Base Node.js image      |
| WORKDIR | Set container directory |
| COPY    | Copy app files          |
| RUN     | Install dependencies    |
| EXPOSE  | App port                |
| CMD     | Start application       |

---

# 4️⃣ Step 3: Build Docker Image

Build image locally.

```bash
docker build -t my-node-app .
```

Check images:

```bash
docker images
```

Example output:

```
REPOSITORY     TAG
my-node-app    latest
node           18
```

---

# 5️⃣ Step 4: Test Container Locally

Run the container to verify it works.

```bash
docker run -d -p 3000:3000 my-node-app
```

Check container:

```bash
docker ps
```

Check logs:

```bash
docker logs container_id
```

Visit in browser:

```
http://localhost:3000
```

---

# 6️⃣ Step 5: Push Code to Git Repository

Push project to GitHub.

Example:

```bash
git init
git add .
git commit -m "initial commit"
git push origin main
```

Repository now contains:

```
App code
Dockerfile
```

---

# 7️⃣ Step 6: CI/CD Pipeline Starts

CI tools detect code changes.

Common tools:

* Jenkins
* GitHub Actions
* GitLab CI
* CircleCI

Pipeline steps:

```
1 Install dependencies
2 Build Docker image
3 Run tests
4 Push Docker image to registry
```

---

# 8️⃣ Step 7: Build Image in CI Pipeline

Example CI command:

```bash
docker build -t username/my-node-app:v1 .
```

Tagging image with version.

Example:

```
username/my-node-app:v1
```

---

# 9️⃣ Step 8: Push Image to Docker Registry

Login first:

```bash
docker login
```

Push image:

```bash
docker push username/my-node-app:v1
```

Image stored in:

* Docker Hub
* AWS ECR
* Google Container Registry
* Azure Container Registry

Now any server can pull this image.

---

# 🔟 Step 9: Deployment Stage

Server pulls the image.

Example:

```bash
docker pull username/my-node-app:v1
```

Run container:

```bash
docker run -d -p 3000:3000 username/my-node-app:v1
```

Application is now live.

---

# 1️⃣1️⃣ Production Deployment (Kubernetes)

In real companies, Docker containers are usually deployed using **Kubernetes**.

Flow:

```
Docker Image
      ↓
Container Registry
      ↓
Kubernetes pulls image
      ↓
Creates Pods
      ↓
Application runs
```

Example Kubernetes command:

```
kubectl apply -f deployment.yaml
```

---

# 1️⃣2️⃣ Monitoring and Logs

DevOps engineers monitor containers.

Commands:

Check logs

```bash
docker logs container_id
```

Check container status

```bash
docker ps
```

Tools used in production:

* Prometheus
* Grafana
* ELK Stack

---

# 1️⃣3️⃣ Real Production DevOps Pipeline Diagram

```
Developer
   ↓
GitHub Repository
   ↓
CI/CD Pipeline
   ↓
Build Docker Image
   ↓
Run Tests
   ↓
Push Image to Registry
   ↓
Deployment Server / Kubernetes
   ↓
Running Containers
   ↓
Monitoring & Logging
```

---

# 1️⃣4️⃣ Real DevOps Tools Used With Docker

| Stage      | Tools                   |
| ---------- | ----------------------- |
| Code       | Git, GitHub             |
| Build      | Docker                  |
| CI/CD      | Jenkins, GitHub Actions |
| Registry   | Docker Hub, AWS ECR     |
| Deployment | Kubernetes              |
| Monitoring | Prometheus, Grafana     |

---

# 1️⃣5️⃣ Commands Used in Real Workflow

Most used commands:

```bash
docker build
docker run
docker ps
docker logs
docker exec
docker tag
docker push
docker pull
docker stop
docker rm
```

---

# ⭐ Example Real DevOps Workflow

Full process:

```
Write code
    ↓
Create Dockerfile
    ↓
docker build
    ↓
docker run (test locally)
    ↓
Push code to GitHub
    ↓
CI/CD builds Docker image
    ↓
docker push to registry
    ↓
Server pulls image
    ↓
Run container
```

---




**Docker Compose** is used to run **multiple containers together** as one application.
In real projects, apps rarely run in a single container. Example:

* Web App (Node.js / Python / Java)
* Database (MySQL / PostgreSQL)
* Cache (Redis)
* Message queue (RabbitMQ)

Instead of running many `docker run` commands, **Docker Compose manages everything using one YAML file**. 🚀

---

# 1️⃣ What is Docker Compose?

**Docker Compose** is a tool that lets you **define and run multi-container Docker applications using a single file** called:

```text
docker-compose.yml
```

With Compose you can start everything using:

```bash
docker compose up
```

Think of it like:

```text
Dockerfile → builds ONE container
Docker Compose → manages MULTIPLE containers
```

---

# 2️⃣ Why Docker Compose is Used

Without Compose:

```bash
docker run -d --name database mysql
docker run -d --name redis redis
docker run -d --name webapp node
```

With Compose:

```bash
docker compose up
```

Everything starts automatically.

Benefits:

✅ Runs multiple containers
✅ Creates network automatically
✅ Easy environment configuration
✅ Good for development and testing

---

# 3️⃣ Basic Docker Compose File Structure

Example `docker-compose.yml`

```yaml
version: "3"

services:

  web:
    image: nginx
    ports:
      - "8080:80"

  redis:
    image: redis
```

Explanation:

| Field    | Meaning               |
| -------- | --------------------- |
| version  | compose version       |
| services | containers definition |
| web      | service name          |
| image    | Docker image          |
| ports    | port mapping          |

---

# 4️⃣ Simple Multi-Container Example

Let's run:

* **Web Server**
* **Database**

Project structure:

```text
project/
 ├── docker-compose.yml
```

Docker Compose file:

```yaml
version: "3"

services:

  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
```

Run application:

```bash
docker compose up
```

Now both containers start.

Check containers:

```bash
docker ps
```

Stop them:

```bash
docker compose down
```

---

# 5️⃣ Real DevOps Example (Web App + Database)

Project structure:

```text
my-app/
 ├── app
 │   ├── app.py
 │   └── Dockerfile
 └── docker-compose.yml
```

---

## Dockerfile (for web app)

```dockerfile
FROM python:3.10

WORKDIR /app

COPY . .

RUN pip install flask

CMD ["python","app.py"]
```

---

## docker-compose.yml

```yaml
version: "3"

services:

  web:
    build: ./app
    ports:
      - "5000:5000"
    depends_on:
      - db

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
```

Explanation:

| Service | Purpose            |
| ------- | ------------------ |
| web     | Python application |
| db      | MySQL database     |

`depends_on` ensures **database starts first**.

---

# 6️⃣ Important Docker Compose Commands

### Start services

```bash
docker compose up
```

Start in background:

```bash
docker compose up -d
```

---

### Stop services

```bash
docker compose down
```

---

### View running containers

```bash
docker compose ps
```

---

### View logs

```bash
docker compose logs
```

Live logs:

```bash
docker compose logs -f
```

---

### Restart services

```bash
docker compose restart
```

---

### Rebuild containers

```bash
docker compose up --build
```

Used when code changes.

---

# 7️⃣ Networking in Docker Compose

Docker Compose automatically creates a **network**.

Example:

```text
web container
      ↓
docker network
      ↓
db container
```

The web app can connect to database using:

```text
db:3306
```

Because service name becomes **hostname**.

Example database connection:

```python
host="db"
```

---

# 8️⃣ Docker Compose with Volumes

Volumes store persistent data.

Example:

```yaml
version: "3"

services:

  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - dbdata:/var/lib/mysql

volumes:
  dbdata:
```

Now database data **won’t disappear if container stops**.

---

# 9️⃣ Real Production Example (3 Containers)

Example:

* React frontend
* Node backend
* MongoDB database

```yaml
version: "3"

services:

  frontend:
    image: nginx
    ports:
      - "3000:80"

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongodb:/data/db

volumes:
  mongodb:
```

---

# 🔟 DevOps Workflow with Docker Compose

Typical developer workflow:

```text
Developer writes code
        ↓
docker-compose.yml defines services
        ↓
docker compose up
        ↓
All containers start
        ↓
Developer tests app locally
```

---

# 1️⃣1️⃣ Difference: Docker vs Docker Compose

| Feature       | Docker            | Docker Compose    |
| ------------- | ----------------- | ----------------- |
| Containers    | Single            | Multiple          |
| Configuration | CLI commands      | YAML file         |
| Use case      | Simple containers | Full applications |

---

# 1️⃣2️⃣ DevOps Engineers Use Compose For

Most common use cases:

* Local development environments
* Integration testing
* Running microservices locally
* Quick container orchestration

Example stack:

```text
App
Database
Redis
Nginx
```

All defined in one Compose file.

---

# ⭐ Most Important Compose Commands

Remember these:

```bash
docker compose up
docker compose up -d
docker compose down
docker compose ps
docker compose logs
docker compose restart
docker compose build
```

---


Docker networking is **one of the most important topics in Docker**, especially for DevOps engineers working with **microservices, Kubernetes, and multi-container apps**. I'll explain it step-by-step so you understand **how containers communicate with each other and with the outside world**. 🌐🐳

---

# 1️⃣ What is Docker Networking?

Docker networking allows **containers to communicate** with:

* Other containers
* The host machine
* External networks (internet)

Example architecture:

```text
User Browser
      ↓
Host Machine (Port 8080)
      ↓
Docker Container (Nginx :80)
      ↓
Another Container (Database :3306)
```

Without networking, containers would be **isolated systems**.

---

# 2️⃣ How Docker Networking Works

When Docker installs, it creates a **virtual network interface**.

Basic flow:

```text
Container
   ↓
Virtual Ethernet (veth)
   ↓
Docker Bridge Network
   ↓
Host Network
   ↓
Internet
```

Each container gets:

* an **IP address**
* a **network interface**
* routing rules

---

# 3️⃣ Types of Docker Networks

Docker provides several network drivers.

| Network Type | Purpose                        |
| ------------ | ------------------------------ |
| bridge       | Default network for containers |
| host         | Container shares host network  |
| none         | No networking                  |
| overlay      | Used in Docker Swarm           |
| macvlan      | Assigns real MAC address       |

Most commonly used:

```text
bridge
host
overlay
```

---

# 4️⃣ Bridge Network (Default)

Bridge is the **default Docker network**.

When you run a container:

```bash
docker run nginx
```

Docker automatically connects it to:

```text
bridge network
```

Check networks:

```bash
docker network ls
```

Example output:

```text
NETWORK ID     NAME      DRIVER
abc123         bridge    bridge
xyz456         host      host
```

---

## How Bridge Network Works

```text
Container A
      ↓
Docker Bridge
      ↓
Container B
```

Each container gets an IP like:

```text
172.17.0.2
172.17.0.3
```

Test communication:

```bash
docker exec -it containerA ping 172.17.0.3
```

But this is **not recommended for production**.

---

# 5️⃣ Custom Bridge Network (Best Practice)

DevOps engineers usually create **custom networks**.

Create network:

```bash
docker network create mynetwork
```

Run containers in this network:

```bash
docker run -d --name web --network mynetwork nginx
```

```bash
docker run -d --name db --network mynetwork mysql
```

Now containers communicate using **container name**.

Example:

```text
web → db
```

Instead of:

```text
172.17.0.3
```

Example connection string:

```text
mysql://db:3306
```

This is how **Docker Compose networking works internally**.

---

# 6️⃣ Host Network

In **host network mode**, container uses the **host machine’s network directly**.

Run container:

```bash
docker run --network host nginx
```

Architecture:

```text
Container
    ↓
Host Network
    ↓
Internet
```

Advantages:

* No port mapping needed
* Faster networking

Disadvantages:

* No isolation
* Security risk

Mostly used in **high-performance systems**.

---

# 7️⃣ None Network

This disables networking.

Run container:

```bash
docker run --network none nginx
```

Container will have:

```text
No internet
No communication
```

Used for:

* security testing
* isolated workloads

---

# 8️⃣ Overlay Network

Overlay networks are used in **Docker Swarm clusters**.

They allow containers across **multiple machines** to communicate.

Architecture:

```text
Server 1
   ↓
Container A
      ↓
Overlay Network
      ↓
Container B
   ↑
Server 2
```

Command:

```bash
docker network create -d overlay myoverlay
```

Used in:

* distributed applications
* container clusters

---

# 9️⃣ Macvlan Network

Macvlan assigns containers **real IP addresses on the local network**.

Example:

```text
Container → 192.168.1.100
Container → 192.168.1.101
```

Create macvlan network:

```bash
docker network create -d macvlan \
--subnet=192.168.1.0/24 \
--gateway=192.168.1.1 \
mymacvlan
```

Used in:

* legacy applications
* network appliances

---

# 🔟 Docker Port Mapping

Containers run on **internal ports**.

Example:

```text
Nginx container → port 80
```

Expose to host:

```bash
docker run -p 8080:80 nginx
```

Mapping:

```text
Host:8080 → Container:80
```

Access via browser:

```text
http://localhost:8080
```

---

# 1️⃣1️⃣ Inspect Docker Network

Check network details:

```bash
docker network inspect bridge
```

Example output:

```text
Containers
Subnet
Gateway
IP range
```

Shows which containers are connected.

---

# 1️⃣2️⃣ Connect Container to Network

Attach container:

```bash
docker network connect mynetwork container1
```

Disconnect container:

```bash
docker network disconnect mynetwork container1
```

---

# 1️⃣3️⃣ Real DevOps Example

Example application:

```text
Frontend (React)
Backend (Node)
Database (MongoDB)
```

Architecture:

```text
React Container
        ↓
Docker Network
        ↓
Node Container
        ↓
MongoDB Container
```

Docker Compose automatically creates this network.

Example Compose networking:

```yaml
services:
  frontend:
    build: ./frontend

  backend:
    build: ./backend

  mongo:
    image: mongo
```

Containers communicate using:

```text
backend → mongo
frontend → backend
```

---

# 1️⃣4️⃣ Common Docker Networking Commands

List networks:

```bash
docker network ls
```

Create network:

```bash
docker network create mynetwork
```

Inspect network:

```bash
docker network inspect mynetwork
```

Delete network:

```bash
docker network rm mynetwork
```

---

# ⭐ Networking Tips for DevOps Engineers

Best practices:

✔ Use **custom bridge networks**
✔ Use **service names instead of IP addresses**
✔ Use **Docker Compose networks**
✔ Avoid default bridge in production

Example production network:

```text
frontend-network
backend-network
database-network
```

---




Docker **Volumes** are extremely important because **containers are temporary**, but applications often need **persistent data** (databases, logs, uploads, etc.). In DevOps and production environments, volumes are used to **store data safely outside containers**. Let's go deep step-by-step. 🐳💾

---

# 1️⃣ Why Docker Volumes Are Needed

By default, container storage is **ephemeral**.

Example:

```bash
docker run -d nginx
```

If you delete the container:

```bash
docker rm container_id
```

All data inside it **disappears**.

Example problem:

```text
MySQL container
   ↓
Database created
   ↓
Container removed
   ↓
Database LOST
```

Volumes solve this.

---

# 2️⃣ What is a Docker Volume?

A **Docker Volume** is a **persistent storage location managed by Docker**.

Architecture:

```
Container
   ↓
Volume
   ↓
Host filesystem
```

Data is stored **outside the container lifecycle**.

Meaning:

* Container can stop
* Container can be deleted
* Data remains safe

---

# 3️⃣ Types of Docker Storage

Docker provides three storage methods.

| Type        | Description            | Production Use |
| ----------- | ---------------------- | -------------- |
| Volumes     | Managed by Docker      | ✅ Best         |
| Bind mounts | Host directory mapping | Sometimes      |
| tmpfs       | Memory storage         | Rare           |

Most production systems use:

```
Docker Volumes
```

---

# 4️⃣ Creating Docker Volumes

Create volume:

```bash
docker volume create myvolume
```

List volumes:

```bash
docker volume ls
```

Example output:

```
DRIVER    VOLUME NAME
local     myvolume
```

Inspect volume:

```bash
docker volume inspect myvolume
```

This shows:

* mount point
* driver
* metadata

---

# 5️⃣ Using Volumes with Containers

Attach volume while running container.

```bash
docker run -d -v myvolume:/app nginx
```

Explanation:

```
myvolume → Docker volume
/app → container directory
```

Architecture:

```
Host
 ↓
Volume (myvolume)
 ↓
Container /app
```

Data written to `/app` goes to the volume.

---

# 6️⃣ Anonymous Volumes

Docker can create volumes automatically.

Example:

```bash
docker run -v /data nginx
```

Docker creates a random volume like:

```
f4a12fbeab21
```

Not recommended in production because it's hard to manage.

---

# 7️⃣ Bind Mounts

Bind mounts map **host directories directly to containers**.

Example:

```bash
docker run -v /home/user/data:/app nginx
```

Architecture:

```
Host Folder /home/user/data
        ↓
Container Folder /app
```

Used when developers want **live file changes**.

Example use cases:

* web development
* configuration files
* code editing

But bind mounts depend on host filesystem structure.

---

# 8️⃣ Docker Volume Commands

List volumes:

```bash
docker volume ls
```

Create volume:

```bash
docker volume create myvolume
```

Inspect volume:

```bash
docker volume inspect myvolume
```

Delete volume:

```bash
docker volume rm myvolume
```

Delete unused volumes:

```bash
docker volume prune
```

---

# 9️⃣ Volumes with Docker Compose

Docker Compose makes volumes easy.

Example:

```yaml
version: "3"

services:

  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - dbdata:/var/lib/mysql

volumes:
  dbdata:
```

Architecture:

```
MySQL Container
      ↓
Volume dbdata
      ↓
Host storage
```

Now if container restarts:

```
Database data stays safe
```

---

# 🔟 Example: MySQL Persistent Data

Run MySQL with volume:

```bash
docker run -d \
-v mysql_data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
mysql
```

Now database files stored in:

```
/var/lib/docker/volumes/mysql_data
```

Container can restart without losing data.

---

# 1️⃣1️⃣ Backup and Restore Volumes

DevOps engineers must **backup production data**.

Backup example:

```bash
docker run --rm \
-v myvolume:/data \
-v $(pwd):/backup \
busybox \
tar czf /backup/backup.tar.gz /data
```

Restore:

```bash
tar xzf backup.tar.gz
```

This is common in **database backups**.

---

# 1️⃣2️⃣ Volume Drivers (Production Storage)

In production environments, volumes are often connected to **external storage systems**.

Examples:

| Driver | Storage         |
| ------ | --------------- |
| local  | host disk       |
| nfs    | network storage |
| rexray | cloud storage   |
| aws    | EBS volumes     |
| azure  | Azure disk      |

Example NFS volume:

```bash
docker volume create \
--driver local \
--opt type=nfs \
--opt o=addr=192.168.1.10 \
--opt device=:/data \
nfsvolume
```

Used in **cluster environments**.

---

# 1️⃣3️⃣ Real Production Example

Example architecture:

```
User
 ↓
Nginx Container
 ↓
App Container
 ↓
Database Container
 ↓
Docker Volume
 ↓
Cloud Storage / Disk
```

Volumes typically store:

```
Database data
User uploads
Logs
Application cache
```

---

# 1️⃣4️⃣ Best Practices for Production Volumes

DevOps engineers follow these rules.

### 1 Use named volumes

Good:

```
db_data
app_logs
uploads
```

Bad:

```
random hash volumes
```

---

### 2 Separate data volumes

Example:

```
database_volume
logs_volume
uploads_volume
```

Do not mix data types.

---

### 3 Backup volumes regularly

Production systems schedule backups using:

```
cron
Kubernetes jobs
backup containers
```

---

### 4 Use external storage for clusters

Example:

```
AWS EBS
NFS
Ceph
GlusterFS
```

Because containers may run on different machines.

---

# 1️⃣5️⃣ Volumes in Kubernetes (Real Production)

In Kubernetes, Docker volumes become:

```
Persistent Volumes (PV)
Persistent Volume Claims (PVC)
```

Architecture:

```
Pod
 ↓
PVC
 ↓
PV
 ↓
Cloud Storage (EBS, NFS, etc)
```

Used for:

* databases
* large applications
* stateful services

---

# 1️⃣6️⃣ Real DevOps Stack Example

Example project:

```
React Frontend
Node Backend
MongoDB Database
```

Docker Compose:

```yaml
services:

  backend:
    build: ./backend

  mongo:
    image: mongo
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```

Now MongoDB data persists.

---

# ⭐ Most Important Volume Commands

These are used frequently in DevOps work.

```bash
docker volume create
docker volume ls
docker volume inspect
docker volume rm
docker volume prune
docker run -v
```

---
**Multi-stage Docker builds** are a very important concept in modern Docker usage. They help create **smaller, secure, and production-ready images** by separating the **build environment** from the **runtime environment**. DevOps engineers use this technique almost everywhere in production pipelines. 🚀

---

# 1️⃣ What Is a Multi-Stage Docker Build?

A **multi-stage build** uses **multiple `FROM` statements** in a single Dockerfile to create different build stages.

Each stage performs a specific task.

Typical flow:

```text
Source Code
     ↓
Build Stage (compile code)
     ↓
Final Stage (only runtime files)
     ↓
Small Production Image
```

This prevents unnecessary tools (like compilers) from being included in the final image.

---

# 2️⃣ Problem Without Multi-Stage Builds

Consider a normal Dockerfile:

```dockerfile
FROM node:18

WORKDIR /app

COPY . .

RUN npm install
RUN npm run build

CMD ["node","server.js"]
```

Issue:

The image contains:

```text
Node runtime
Build tools
Source code
Dependencies
Temporary files
```

Final image becomes **large and inefficient**.

Example size:

```text
1GB image
```

---

# 3️⃣ Solution: Multi-Stage Build

Use separate stages:

```dockerfile
# Build stage
FROM node:18 AS builder

WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

# Production stage
FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist

CMD ["node","dist/server.js"]
```

Explanation:

| Stage       | Purpose             |
| ----------- | ------------------- |
| builder     | compile application |
| final image | run application     |

Only **compiled files** move to the final image.

---

# 4️⃣ How `COPY --from` Works

This command copies files **from one stage to another**.

Example:

```dockerfile
COPY --from=builder /app/dist ./dist
```

Meaning:

```text
builder stage
   ↓
/app/dist
   ↓
final container
```

This keeps the final image **clean and minimal**.

---

# 5️⃣ Multi-Stage Build Architecture

```text
Stage 1 (builder)
------------------
Node image
Install dependencies
Build application

        ↓

Stage 2 (production)
---------------------
Lightweight image
Copy compiled files
Run application
```

Benefits:

```text
Smaller images
Better security
Faster deployments
```

---

# 6️⃣ Real Example: Go Application

Go apps are perfect for multi-stage builds.

Dockerfile:

```dockerfile
# Build stage
FROM golang:1.20 AS builder

WORKDIR /app
COPY . .

RUN go build -o app

# Runtime stage
FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/app .

CMD ["./app"]
```

Explanation:

Stage 1:

```text
Compile Go binary
```

Stage 2:

```text
Run compiled binary only
```

Final image becomes extremely small.

Example:

```text
Without multi-stage → 1GB
With multi-stage → 20MB
```

---

# 7️⃣ Real Example: React Application

React apps require a **build step**.

Dockerfile:

```dockerfile
# Build stage
FROM node:18 AS build

WORKDIR /app
COPY . .

RUN npm install
RUN npm run build

# Production stage
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```

Stages:

| Stage | Action             |
| ----- | ------------------ |
| build | build React app    |
| nginx | serve static files |

Final container only contains:

```text
HTML
CSS
JavaScript
```

Not the Node build environment.

---

# 8️⃣ Multi-Stage Build with Python

Example Python app:

```dockerfile
# Build stage
FROM python:3.10 AS builder

WORKDIR /app

COPY requirements.txt .
RUN pip install --user -r requirements.txt

# Runtime stage
FROM python:3.10-slim

WORKDIR /app

COPY --from=builder /root/.local /root/.local
COPY . .

CMD ["python","app.py"]
```

This keeps runtime smaller.

---

# 9️⃣ Benefits of Multi-Stage Builds

### 1️⃣ Smaller images

Example:

```text
Before → 800MB
After → 120MB
```

Smaller images mean:

* faster CI/CD
* faster deployments

---

### 2️⃣ Better security

Final image does NOT include:

```text
compilers
build tools
source code
```

Attack surface becomes smaller.

---

### 3️⃣ Faster builds

Docker caching works better with separated stages.

---

### 4️⃣ Cleaner production images

Only required files exist.

---

# 🔟 Multi-Stage Builds in CI/CD

Typical DevOps pipeline:

```text
Developer pushes code
      ↓
CI pipeline starts
      ↓
Docker build (multi-stage)
      ↓
Small optimized image created
      ↓
Push to registry
      ↓
Deploy to Kubernetes
```

Example CI command:

```bash
docker build -t myapp:v1 .
```

CI automatically runs the multi-stage Dockerfile.

---

# 1️⃣1️⃣ Best Practices for Multi-Stage Builds

### Use lightweight runtime images

Example:

```dockerfile
FROM node:18-alpine
```

Instead of:

```dockerfile
FROM node:18
```

---

### Use named stages

Example:

```dockerfile
FROM node:18 AS builder
```

Better than referencing by index.

---

### Copy only required files

Bad:

```dockerfile
COPY --from=builder /app .
```

Good:

```dockerfile
COPY --from=builder /app/dist ./dist
```

---

# 1️⃣2️⃣ Advanced Multi-Stage Example

Large applications sometimes have **3 stages**.

```dockerfile
FROM node:18 AS dependencies
WORKDIR /app
COPY package.json .
RUN npm install

FROM node:18 AS build
WORKDIR /app
COPY . .
COPY --from=dependencies /app/node_modules ./node_modules
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

Stages:

```text
dependencies
build
production
```

---

# ⭐ Why DevOps Engineers Love Multi-Stage Builds

Because they help achieve:

```text
Small Docker images
Secure production containers
Faster deployments
Efficient CI/CD pipelines
```

Most **modern Dockerfiles use multi-stage builds**.

---
Docker becomes **really powerful in CI/CD pipelines** because it ensures the same environment in **development → testing → production**. DevOps engineers often integrate Docker with tools like **Jenkins** and **GitHub Actions** to automate builds, tests, and deployments.

Below is a **complete DevOps-level explanation** of **Docker + CI/CD workflows**.

---

# Docker + CI/CD (DevOps Workflow)

## 1. What CI/CD Means

**CI – Continuous Integration**

* Developers push code frequently
* Pipeline automatically **builds + tests the application**

**CD – Continuous Deployment/Delivery**

* After successful build/test
* Application is **automatically deployed**

Docker helps because the application runs inside **containers**, which guarantees consistency.

**Without Docker**

```
Dev machine → Works
Test server → Breaks
Production → Different environment
```

**With Docker**

```
Dev → Container
Test → Same Container
Production → Same Container
```

---

# Typical DevOps Pipeline With Docker

```
Developer pushes code → GitHub
        ↓
CI/CD pipeline triggers
        ↓
Build Docker image
        ↓
Run tests in container
        ↓
Push image to Docker Registry
        ↓
Deploy container to server
```

Example Registry:

* **Docker Hub**
* **Amazon Elastic Container Registry**
* **Google Container Registry**

---

# Step-by-Step Real DevOps Example

## Step 1: Developer Pushes Code

```
git push origin main
```

This triggers the pipeline.

---

# CI/CD With GitHub Actions + Docker

**Repository structure**

```
project/
 ├── app.py
 ├── requirements.txt
 ├── Dockerfile
 └── .github/workflows/docker.yml
```

---

# GitHub Actions Docker Pipeline

File:

```
.github/workflows/docker.yml
```

name: Docker CI/CD Pipeline

on:
push:
branches: [ "main" ]

jobs:
build:
runs-on: ubuntu-latest

```
steps:

- name: Checkout Code
  uses: actions/checkout@v3

- name: Login to DockerHub
  uses: docker/login-action@v2
  with:
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}

- name: Build Docker Image
  run: docker build -t myusername/myapp:latest .

- name: Push Image
  run: docker push myusername/myapp:latest
```

---

# What Happens Here

### Step 1

```
Checkout Code
```

GitHub downloads your repository.

---

### Step 2

```
Docker Login
```

Pipeline logs into Docker registry.

---

### Step 3

```
docker build
```

Builds image from Dockerfile.

---

### Step 4

```
docker push
```

Uploads image to registry.

---

# Final Result

```
Docker Hub
   ↓
myusername/myapp:latest
```

Image is ready for deployment.

---

# CI/CD With Jenkins + Docker

Another very common DevOps setup uses **Jenkins**.

Pipeline file:

```
Jenkinsfile
```

Example:

pipeline {
agent any

```
stages {

    stage('Clone Repo') {
        steps {
            git 'https://github.com/user/project.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t myapp .'
        }
    }

    stage('Test') {
        steps {
            sh 'docker run myapp pytest'
        }
    }

    stage('Push Image') {
        steps {
            sh 'docker tag myapp username/myapp'
            sh 'docker push username/myapp'
        }
    }

    stage('Deploy') {
        steps {
            sh 'docker run -d -p 80:80 username/myapp'
        }
    }
}
```

}

---

# What DevOps Engineers Automate

### Build

```
docker build
```

### Test

```
docker run tests
```

### Tag image

```
docker tag app:v1
```

### Push image

```
docker push
```

### Deploy container

```
docker run -d
```

---

# Production Deployment Methods

## 1️⃣ Direct Docker

```
docker run -d -p 80:80 myapp
```

Simple servers.

---

## 2️⃣ Docker Compose

```
docker-compose up -d
```

Multi-service apps.

---

## 3️⃣ Kubernetes (Most common)

Production systems use **Kubernetes**.

Pipeline:

```
Build Image
     ↓
Push to Registry
     ↓
kubectl apply deployment.yaml
```

---

# Example Production Workflow

```
Developer pushes code
        ↓
GitHub Actions builds Docker image
        ↓
Image pushed to Docker Hub
        ↓
Kubernetes pulls image
        ↓
Pods updated automatically
```

---

# Important Docker Tags In CI/CD

Instead of only `latest`, DevOps engineers use versions.

Example:

```
myapp:1.0
myapp:1.1
myapp:prod
myapp:staging
myapp:dev
```

Pipeline example:

```
docker build -t myapp:${{ github.sha }}
```

This tags image with commit hash.

---

# Security Best Practices

### 1. Scan Images

Tools:

* **Trivy**
* **Snyk**

Example:

```
trivy image myapp
```

---

### 2. Use small images

Prefer

```
alpine
distroless
```

Instead of

```
ubuntu
```

---

### 3. Never store secrets in images

Use:

```
environment variables
secret managers
```

---

# CI/CD Pipeline Architecture (Real DevOps)

```
GitHub
  ↓
CI/CD Pipeline
  ↓
Docker Build
  ↓
Docker Registry
  ↓
Deployment
  ↓
Kubernetes / Servers
```

---

# Skills DevOps Engineers Use With Docker

You already learned many of them:

Docker
Dockerfile
Multi-stage builds
Docker Compose
Volumes
Networking

Next big skills:

1️⃣ **Kubernetes**
2️⃣ **Helm**
3️⃣ **Terraform**
4️⃣ **Prometheus**

---

# The Complete Docker Learning Path (DevOps)

```
Docker Basics
     ↓
Dockerfile
     ↓
Docker Networking
     ↓
Docker Volumes
     ↓
Docker Compose
     ↓
Multi-stage Builds
     ↓
Docker + CI/CD
     ↓
Kubernetes
```

---
Docker image optimization is **very important in real DevOps environments** because smaller images mean:

⚡ Faster CI/CD builds
⚡ Faster container startup
⚡ Lower storage cost
⚡ Better security (less attack surface)

Many companies reduce images from **1GB → 100MB or even 20MB** using optimization techniques.

Let’s go through the **most important Docker image optimization techniques used by DevOps engineers.**

---

# 1. Use Smaller Base Images

Your **base image determines most of the image size**.

### Example (Bad)

```dockerfile
FROM ubuntu
```

Ubuntu image ≈ **70–80MB**

---

### Better

```dockerfile
FROM node:alpine
```

Alpine-based images are **very small (~5MB)**.

---

### Common Small Images

| Base Image  | Size  | Usage             |
| ----------- | ----- | ----------------- |
| alpine      | ~5MB  | lightweight Linux |
| debian-slim | ~20MB | minimal Debian    |
| distroless  | ~10MB | production apps   |

Example:

```dockerfile
FROM python:3.10-alpine
```

---

# 2. Use Multi-Stage Builds (MOST IMPORTANT)

Instead of including build tools in the final image, use **multiple stages**.

### Without Multi-Stage

```dockerfile
FROM node:18

WORKDIR /app

COPY . .

RUN npm install

CMD ["node", "app.js"]
```

Problem:
Includes **build dependencies** in final image.

---

### Optimized Multi-Stage

```dockerfile
# Build stage
FROM node:18 as builder

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .

# Production stage
FROM node:18-alpine

WORKDIR /app
COPY --from=builder /app .

CMD ["node", "app.js"]
```

Result:

```
Original image: ~900MB
Optimized: ~150MB
```

---

# 3. Combine RUN Commands

Each `RUN` creates a **new layer**.

Bad example:

```dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y vim
```

Creates **3 layers**.

---

Better:

```dockerfile
RUN apt-get update && \
    apt-get install -y curl vim
```

Single layer = smaller image.

---

# 4. Remove Unnecessary Files

Package managers leave cache files.

Example:

```dockerfile
RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*
```

This removes package cache.

---

For Alpine:

```dockerfile
RUN apk add --no-cache curl
```

---

# 5. Use `.dockerignore`

Just like `.gitignore`, it prevents unnecessary files from being copied.

Example `.dockerignore`

```
node_modules
.git
.gitignore
README.md
tests
logs
.env
```

Without this, Docker may copy **huge unnecessary folders**.

---

# 6. Copy Only Necessary Files

Bad:

```dockerfile
COPY . .
```

Copies **everything**.

---

Better:

```dockerfile
COPY package.json .
COPY src/ ./src
```

Only copy required files.

---

# 7. Use Specific Image Tags

Bad:

```dockerfile
FROM node:latest
```

Problems:

* Unpredictable builds
* Large images

---

Better:

```dockerfile
FROM node:18-alpine
```

Stable and smaller.

---

# 8. Avoid Installing Unnecessary Packages

Example bad Dockerfile:

```dockerfile
RUN apt-get install -y \
    vim \
    curl \
    net-tools \
    gcc \
    make
```

Many packages are **not required in production**.

Only install what your app needs.

---

# 9. Use Distroless Images (Production)

Distroless images contain **only the application runtime**.

Example:

```dockerfile
FROM gcr.io/distroless/nodejs
```

Advantages:

* Smaller
* More secure
* No shell access

Popular in **Kubernetes** environments.

---

# 10. Use Docker Image Layer Caching

Order your Dockerfile for caching.

Bad order:

```dockerfile
COPY . .
RUN npm install
```

Every code change **reinstalls dependencies**.

---

Better:

```dockerfile
COPY package.json .
RUN npm install

COPY . .
```

Dependencies cached → faster builds.

---

# Example: Optimized Node.js Dockerfile

```dockerfile
# Stage 1 - Builder
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

# Stage 2 - Production
FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules

CMD ["node", "dist/app.js"]
```

Benefits:

✔ Small image
✔ Fast build
✔ No dev dependencies

---

# Image Optimization Tools (Used in DevOps)

### Docker image inspection

```bash
docker history image-name
```

Shows layer sizes.

---

### Security + size scanning tools

* **Trivy**
* **Docker Scout**
* **Dive**

Example:

```bash
dive my-image
```

Shows which layers consume the most space.

---

# Real Example Optimization

Before optimization:

```
Image size: 1.2GB
Build time: 6 minutes
```

After optimization:

```
Image size: 180MB
Build time: 2 minutes
```

This is **very common in real DevOps pipelines** using tools like **Jenkins** or **GitHub Actions**.

---

# Docker Image Optimization Checklist

Always check:

✔ Use **alpine or slim images**
✔ Use **multi-stage builds**
✔ Combine RUN commands
✔ Remove package caches
✔ Use `.dockerignore`
✔ Install only necessary packages
✔ Optimize Dockerfile layer order

---
Docker security is **crucial for production DevOps** because containers share the host OS kernel. A small misconfiguration can lead to **container escape, data leaks, or compromised systems**. Below is a **comprehensive, real-world DevOps guide** to Docker security best practices. 🛡️🐳

---

# 1️⃣ Use Minimal Base Images

**Why:** Fewer packages = smaller attack surface.

* Avoid full OS images like `ubuntu` if possible.
* Prefer **`alpine`**, **`distroless`**, or **slim variants**.

Example:

```dockerfile
FROM python:3.10-alpine
```

Benefits:

* Smaller size
* Fewer vulnerabilities
* Faster builds and startup

---

# 2️⃣ Run Containers as Non-Root

**Default:** Most containers run as root → security risk.

**Solution:** Create a user inside Dockerfile.

```dockerfile
FROM node:18-alpine

# Create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

WORKDIR /app
COPY . .

USER appuser

CMD ["node", "app.js"]
```

Benefits:

* Limits what a compromised container can do
* Prevents host file system access

---

# 3️⃣ Limit Container Capabilities

Docker containers inherit many Linux capabilities by default. Limit them:

```bash
docker run --cap-drop ALL --cap-add NET_BIND_SERVICE myapp
```

* Drops unnecessary privileges
* Keeps only what’s needed

---

# 4️⃣ Avoid Storing Secrets in Images

**Bad practice:** Writing passwords/API keys in Dockerfile.

**Better alternatives:**

* **Environment variables** (but don't commit in code)
* **Docker secrets** (especially with Docker Swarm)
* **Secret managers** like AWS Secrets Manager, HashiCorp Vault

Example using Docker secrets:

```bash
docker secret create db_password ./db_password.txt
```

Then in Compose:

```yaml
services:
  db:
    image: mysql
    secrets:
      - db_password

secrets:
  db_password:
    external: true
```

---

# 5️⃣ Keep Images Updated

* Use specific version tags, not `latest`.
* Regularly scan and update images for **security patches**.

```bash
docker pull node:18-alpine
```

**Automate** updates in CI/CD pipelines.

---

# 6️⃣ Scan Images for Vulnerabilities

Tools:

* **Trivy** → fast vulnerability scanning
* **Snyk**
* **Docker Scout**

Example:

```bash
trivy image myapp:latest
```

Scan base images and your own images before deployment.

---

# 7️⃣ Use Read-Only File Systems

Prevent apps from writing everywhere:

```bash
docker run --read-only myapp
```

* Use volumes for writable directories
* Prevents malicious writes inside the container

---

# 8️⃣ Limit Resource Usage

Prevent a container from consuming all host resources:

```bash
docker run --memory="512m" --cpus="1.0" myapp
```

* Avoid DoS attacks from rogue containers
* Essential for multi-tenant environments

---

# 9️⃣ Network Security

* **Use custom bridge networks** instead of default `bridge`.
* **Isolate containers** by network segmentation.
* Avoid exposing ports to the public unnecessarily.

Example Docker Compose:

```yaml
services:
  app:
    image: myapp
    networks:
      - internal
networks:
  internal:
    driver: bridge
```

* Expose only necessary ports with `ports:` mapping

---

# 🔟 Use Docker Content Trust (DCT)

DCT ensures **image integrity**:

```bash
export DOCKER_CONTENT_TRUST=1
docker pull myapp:latest
```

* Only signed images are pulled
* Prevents tampering

---

# 1️⃣1️⃣ Avoid Privileged Mode

**Bad practice:**

```bash
docker run --privileged myapp
```

* Gives full host access → huge risk

**Use only when absolutely required.**

---

# 1️⃣2️⃣ Log and Monitor Containers

* Monitor container logs for unusual behavior.
* Tools: **Prometheus + Grafana**, **Falco** (container runtime security).

Example with Falco:

```bash
falco --docker
```

* Detects unexpected container actions

---

# 1️⃣3️⃣ Minimize Installed Packages

* Only install what's required for runtime.
* Remove build tools in **multi-stage builds**.

Example:

```dockerfile
FROM golang:1.20 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM alpine
COPY --from=builder /app/myapp /myapp
CMD ["/myapp"]
```

* Final image **doesn’t include compilers or dev tools**

---

# 1️⃣4️⃣ Regularly Audit Containers

Check:

```bash
docker ps -a
docker images
docker inspect <container>
```

* Remove unused containers/images
* Keep host clean → reduces attack surface

---

# 1️⃣5️⃣ Use Namespaces and Cgroups (Kernel Security)

* Docker uses **Linux namespaces** → container isolation
* **Cgroups** limit resources
* Ensure host kernel is up-to-date and hardened

---

# 1️⃣6️⃣ Summary Checklist for DevOps

✅ Use minimal base images (`alpine`, `distroless`)
✅ Run as non-root user
✅ Drop unnecessary Linux capabilities
✅ Don’t store secrets in images
✅ Scan images regularly (`Trivy`, `Snyk`)
✅ Keep images updated
✅ Read-only file system + volumes
✅ Limit CPU & memory
✅ Use custom networks
✅ Avoid privileged mode
✅ Multi-stage builds to remove dev tools
✅ Audit and monitor containers

---

# Real DevOps Production Workflow (Docker Security)

```text
Developer pushes code → CI/CD pipeline
        ↓
Docker build (multi-stage, minimal image)
        ↓
Scan image with Trivy/Snyk
        ↓
Push to private registry (Docker Hub/ECR/GCR)
        ↓
Deploy on secured network (custom bridge)
        ↓
Monitor containers (Falco/Prometheus)
```

This is **what real DevOps engineers do in companies** for production.

---
Docker registries are a **core part of the DevOps workflow** because they act as centralized repositories for storing and distributing Docker images. In real production environments, DevOps engineers use **private and cloud registries** like **ECR, GCR, and ACR** for secure, scalable deployments. Let’s break it down. 🐳☁️

---

# 1️⃣ What is a Docker Registry?

A **Docker registry** is a storage and distribution system for Docker images.

* **Docker Hub** → public registry (default)
* **Private registries** → secure for company/internal use

**Role in DevOps pipelines:**

```text id="y9d9we"
Build Docker image → Push to registry → Pull image in production → Deploy container
```

---

# 2️⃣ Types of Docker Registries

| Registry   | Type             | Provider     | Notes                                                |
| ---------- | ---------------- | ------------ | ---------------------------------------------------- |
| Docker Hub | Public / Private | Docker       | Default registry, free for small projects            |
| ECR        | Private          | AWS          | Fully managed, integrates with IAM & ECS/EKS         |
| GCR        | Private          | Google Cloud | Integrates with GCP & GKE                            |
| ACR        | Private          | Azure        | Integrates with AKS & Azure AD                       |
| Harbor     | Private          | Open Source  | Enterprise-ready, with RBAC & vulnerability scanning |

---

# 3️⃣ AWS ECR (Elastic Container Registry)

**Use case:** Deploy containers to **AWS ECS, EKS, or EC2**.

### Steps:

1️⃣ **Create repository** in ECR:

```bash id="ecr1"
aws ecr create-repository --repository-name myapp
```

2️⃣ **Login to ECR** (obtain auth token):

```bash id="ecr2"
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com
```

3️⃣ **Tag Docker image**:

```bash id="ecr3"
docker tag myapp:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
```

4️⃣ **Push image**:

```bash id="ecr4"
docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
```

5️⃣ **Pull image for deployment**:

```bash id="ecr5"
docker pull <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
```

**Advantages:**

* IAM integration
* High security
* Works with ECS/EKS

---

# 4️⃣ GCR (Google Container Registry)

**Use case:** Deploy to **GCP + GKE**.

### Steps:

1️⃣ **Enable GCR API**:

```bash id="gcr1"
gcloud services enable containerregistry.googleapis.com
```

2️⃣ **Configure Docker authentication**:

```bash id="gcr2"
gcloud auth configure-docker
```

3️⃣ **Tag image**:

```bash id="gcr3"
docker tag myapp gcr.io/<project-id>/myapp:latest
```

4️⃣ **Push image**:

```bash id="gcr4"
docker push gcr.io/<project-id>/myapp:latest
```

5️⃣ **Pull image**:

```bash id="gcr5"
docker pull gcr.io/<project-id>/myapp:latest
```

**Advantages:**

* Native integration with GKE
* IAM permissions
* Geo-redundancy

---

# 5️⃣ ACR (Azure Container Registry)

**Use case:** Deploy containers to **Azure Kubernetes Service (AKS)** or App Service.

### Steps:

1️⃣ **Create registry**:

```bash id="acr1"
az acr create --resource-group myResourceGroup --name myRegistry --sku Basic
```

2️⃣ **Login to ACR**:

```bash id="acr2"
az acr login --name myRegistry
```

3️⃣ **Tag image**:

```bash id="acr3"
docker tag myapp myregistry.azurecr.io/myapp:latest
```

4️⃣ **Push image**:

```bash id="acr4"
docker push myregistry.azurecr.io/myapp:latest
```

5️⃣ **Pull image**:

```bash id="acr5"
docker pull myregistry.azurecr.io/myapp:latest
```

**Advantages:**

* Azure AD authentication
* Integrated with AKS
* Private and secure

---

# 6️⃣ Docker Registry Commands (Common Across All Registries)

| Command                                    | Description              |
| ------------------------------------------ | ------------------------ |
| `docker login <registry>`                  | Authenticate to registry |
| `docker build -t <image>`                  | Build image with tag     |
| `docker tag <image> <registry>/<repo>:tag` | Tag for registry         |
| `docker push <registry>/<repo>:tag`        | Push image to registry   |
| `docker pull <registry>/<repo>:tag`        | Pull image from registry |
| `docker logout <registry>`                 | Logout from registry     |

---

# 7️⃣ Best Practices for Docker Registries (DevOps)

✅ **Use private registries** for production
✅ **Tag images by version or commit hash**, not just `latest`
✅ **Scan images for vulnerabilities** before pushing (`Trivy`, `Snyk`)
✅ **Enable role-based access (RBAC)** for security
✅ **Use automated CI/CD pipelines** to build, tag, and push images
✅ **Clean up old images** to save space

---

# 8️⃣ Real DevOps CI/CD Flow With Docker Registries

```text id="f1m5e9"
Developer pushes code
        ↓
CI/CD pipeline builds Docker image
        ↓
Scan image for vulnerabilities
        ↓
Tag image (commit hash)
        ↓
Push to Docker registry (ECR/GCR/ACR)
        ↓
Deploy container from registry to production (Kubernetes, ECS, AKS, GKE)
```

Key points:

* Only **trusted, scanned images** go to production
* Images are **versioned and immutable**
* Registries provide **centralized, secure storage**

---

# 9️⃣ Tips for Production DevOps

* Automate tagging by **commit hash or build number**
* Use **image retention policies** to delete old images
* Enable **encryption at rest** for cloud registries
* Integrate registry scans into **CI/CD pipelines**
* Consider **geo-replicated registries** for multi-region deployments

---

✅ Once you master Docker registries, you can handle:

* Private image storage
* Version control of Docker images
* Secure and automated deployments

---
---
---
---
---
---
---

---


---


---


---


---


---


---


---


---


---





Kubernetes (often abbreviated as **K8s**) is the **de facto container orchestration platform** used in production to deploy, scale, and manage containerized applications. For a DevOps engineer, understanding Kubernetes is crucial after mastering Docker. Let’s break it down step by step. 🐳➡️☸️

---

# 1️⃣ What is Kubernetes?

**Kubernetes** is an open-source platform for:

* **Deploying containers**
* **Scaling applications automatically**
* **Managing container lifecycle**
* **Self-healing** (restarting failed containers, rescheduling)

Analogy:

```text id="k8s1"
Docker handles 1 container → Kubernetes handles thousands of containers across multiple servers
```

---

# 2️⃣ Why Kubernetes?

| Problem                                 | How Kubernetes solves it             |
| --------------------------------------- | ------------------------------------ |
| Multiple containers on multiple servers | Cluster management and scheduling    |
| High availability                       | Self-healing, auto-restart, replicas |
| Scaling apps                            | Horizontal Pod Autoscaler (HPA)      |
| Service discovery                       | Internal DNS and load balancing      |
| Rolling updates                         | Deploy new versions without downtime |

---

# 3️⃣ Kubernetes Architecture

Kubernetes cluster has **2 main components**:

### a) Control Plane (Master Node)

Responsible for managing the cluster:

| Component                   | Role                                          |
| --------------------------- | --------------------------------------------- |
| **kube-apiserver**          | Handles API requests                          |
| **etcd**                    | Key-value store for cluster state             |
| **kube-scheduler**          | Assigns pods to nodes                         |
| **kube-controller-manager** | Maintains desired state (replicas, endpoints) |

---

### b) Worker Nodes

Run the actual application containers:

| Component             | Role                                       |
| --------------------- | ------------------------------------------ |
| **kubelet**           | Agent that communicates with control plane |
| **kube-proxy**        | Handles networking & load balancing        |
| **Container runtime** | Docker, containerd, or CRI-O               |

---

# 4️⃣ Kubernetes Objects (Key Concepts)

## 4.1 Pods

* **Smallest deployable unit**
* Usually **1 container**, sometimes multiple containers that share resources

```yaml id="k8s2"
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: myapp
      image: nginx:alpine
      ports:
        - containerPort: 80
```

---

## 4.2 ReplicaSets

* Ensure **a specified number of pod replicas** are running
* Self-healing: recreates pods if a pod dies

```yaml id="k8s3"
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:alpine
```

---

## 4.3 Deployments

* **Manage ReplicaSets & rolling updates**
* Most common way to deploy apps

```yaml id="k8s4"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:alpine
```

---

## 4.4 Services

* **Expose pods** inside/outside cluster
* Types: ClusterIP, NodePort, LoadBalancer

Example LoadBalancer service:

```yaml id="k8s5"
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

---

## 4.5 ConfigMaps & Secrets

* **ConfigMap** → Store app config (non-sensitive)
* **Secret** → Store passwords, tokens, keys

Example Secret:

```yaml id="k8s6"
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: cGFzc3dvcmQ=  # base64 encoded
```

---

## 4.6 Persistent Volumes (PV) & Persistent Volume Claims (PVC)

* Store **data outside pods**, survives pod restarts
* Similar to Docker volumes in production

Example PVC:

```yaml id="k8s7"
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myapp-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

# 5️⃣ Kubernetes Namespaces

* Logical **separation of resources** inside a cluster
* Useful for **multi-team or multi-env setups**

```bash id="k8s8"
kubectl create namespace dev
kubectl create namespace prod
```

---

# 6️⃣ Scaling in Kubernetes

### Manual scaling

```bash id="k8s9"
kubectl scale deployment myapp-deploy --replicas=5
```

### Automatic scaling (HPA)

```bash id="k8s10"
kubectl autoscale deployment myapp-deploy --cpu-percent=50 --min=2 --max=10
```

---

# 7️⃣ Rolling Updates & Rollbacks

**Rolling Update:**

```bash id="k8s11"
kubectl set image deployment/myapp-deploy myapp=nginx:1.21
```

* Updates pods gradually
* No downtime

**Rollback:**

```bash id="k8s12"
kubectl rollout undo deployment/myapp-deploy
```

* Rollback to previous version if issues

---

# 8️⃣ Kubernetes CLI Basics (`kubectl`)

| Command                             | Purpose                 |
| ----------------------------------- | ----------------------- |
| `kubectl get pods`                  | List pods               |
| `kubectl get deployments`           | List deployments        |
| `kubectl describe pod <pod>`        | Detailed info           |
| `kubectl logs <pod>`                | Pod logs                |
| `kubectl exec -it <pod> -- /bin/sh` | Enter pod shell         |
| `kubectl apply -f <file>`           | Create/update resources |
| `kubectl delete -f <file>`          | Delete resources        |

---

# 9️⃣ Kubernetes Networking Basics

* **Pod-to-Pod:** Each pod gets its own IP
* **Service:** Provides stable IP or DNS name
* **Ingress:** Manages external HTTP/HTTPS access

Example: Ingress for HTTP routing

```yaml id="k8s13"
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: myapp-service
            port:
              number: 80
```

---

# 1️⃣0️⃣ Real DevOps Kubernetes Workflow

```text id="k8s14"
Developer pushes code → CI/CD pipeline builds Docker image → Push to registry → 
Kubernetes Deployment pulls image → Pods created → Exposed via Service/Ingress → Scaled automatically → Monitored
```

* **Pod** = container unit
* **Deployment** = manages pods & updates
* **Service** = exposes pods
* **Ingress** = external access
* **PVC/PV** = persistent storage

---




Kubernetes (often abbreviated as **K8s**) is the **de facto container orchestration platform** used in production to deploy, scale, and manage containerized applications. For a DevOps engineer, understanding Kubernetes is crucial after mastering Docker. Let’s break it down step by step. 🐳➡️☸️

---

# 1️⃣ What is Kubernetes?

**Kubernetes** is an open-source platform for:

* **Deploying containers**
* **Scaling applications automatically**
* **Managing container lifecycle**
* **Self-healing** (restarting failed containers, rescheduling)

Analogy:

```text id="k8s1"
Docker handles 1 container → Kubernetes handles thousands of containers across multiple servers
```

---

# 2️⃣ Why Kubernetes?

| Problem                                 | How Kubernetes solves it             |
| --------------------------------------- | ------------------------------------ |
| Multiple containers on multiple servers | Cluster management and scheduling    |
| High availability                       | Self-healing, auto-restart, replicas |
| Scaling apps                            | Horizontal Pod Autoscaler (HPA)      |
| Service discovery                       | Internal DNS and load balancing      |
| Rolling updates                         | Deploy new versions without downtime |

---

# 3️⃣ Kubernetes Architecture

Kubernetes cluster has **2 main components**:

### a) Control Plane (Master Node)

Responsible for managing the cluster:

| Component                   | Role                                          |
| --------------------------- | --------------------------------------------- |
| **kube-apiserver**          | Handles API requests                          |
| **etcd**                    | Key-value store for cluster state             |
| **kube-scheduler**          | Assigns pods to nodes                         |
| **kube-controller-manager** | Maintains desired state (replicas, endpoints) |

---

### b) Worker Nodes

Run the actual application containers:

| Component             | Role                                       |
| --------------------- | ------------------------------------------ |
| **kubelet**           | Agent that communicates with control plane |
| **kube-proxy**        | Handles networking & load balancing        |
| **Container runtime** | Docker, containerd, or CRI-O               |

---

# 4️⃣ Kubernetes Objects (Key Concepts)

## 4.1 Pods

* **Smallest deployable unit**
* Usually **1 container**, sometimes multiple containers that share resources

```yaml id="k8s2"
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: myapp
      image: nginx:alpine
      ports:
        - containerPort: 80
```

---

## 4.2 ReplicaSets

* Ensure **a specified number of pod replicas** are running
* Self-healing: recreates pods if a pod dies

```yaml id="k8s3"
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:alpine
```

---

## 4.3 Deployments

* **Manage ReplicaSets & rolling updates**
* Most common way to deploy apps

```yaml id="k8s4"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:alpine
```

---

## 4.4 Services

* **Expose pods** inside/outside cluster
* Types: ClusterIP, NodePort, LoadBalancer

Example LoadBalancer service:

```yaml id="k8s5"
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

---

## 4.5 ConfigMaps & Secrets

* **ConfigMap** → Store app config (non-sensitive)
* **Secret** → Store passwords, tokens, keys

Example Secret:

```yaml id="k8s6"
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: cGFzc3dvcmQ=  # base64 encoded
```

---

## 4.6 Persistent Volumes (PV) & Persistent Volume Claims (PVC)

* Store **data outside pods**, survives pod restarts
* Similar to Docker volumes in production

Example PVC:

```yaml id="k8s7"
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myapp-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

# 5️⃣ Kubernetes Namespaces

* Logical **separation of resources** inside a cluster
* Useful for **multi-team or multi-env setups**

```bash id="k8s8"
kubectl create namespace dev
kubectl create namespace prod
```

---

# 6️⃣ Scaling in Kubernetes

### Manual scaling

```bash id="k8s9"
kubectl scale deployment myapp-deploy --replicas=5
```

### Automatic scaling (HPA)

```bash id="k8s10"
kubectl autoscale deployment myapp-deploy --cpu-percent=50 --min=2 --max=10
```

---

# 7️⃣ Rolling Updates & Rollbacks

**Rolling Update:**

```bash id="k8s11"
kubectl set image deployment/myapp-deploy myapp=nginx:1.21
```

* Updates pods gradually
* No downtime

**Rollback:**

```bash id="k8s12"
kubectl rollout undo deployment/myapp-deploy
```

* Rollback to previous version if issues

---

# 8️⃣ Kubernetes CLI Basics (`kubectl`)

| Command                             | Purpose                 |
| ----------------------------------- | ----------------------- |
| `kubectl get pods`                  | List pods               |
| `kubectl get deployments`           | List deployments        |
| `kubectl describe pod <pod>`        | Detailed info           |
| `kubectl logs <pod>`                | Pod logs                |
| `kubectl exec -it <pod> -- /bin/sh` | Enter pod shell         |
| `kubectl apply -f <file>`           | Create/update resources |
| `kubectl delete -f <file>`          | Delete resources        |

---

# 9️⃣ Kubernetes Networking Basics

* **Pod-to-Pod:** Each pod gets its own IP
* **Service:** Provides stable IP or DNS name
* **Ingress:** Manages external HTTP/HTTPS access

Example: Ingress for HTTP routing

```yaml id="k8s13"
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: myapp-service
            port:
              number: 80
```

---

# 1️⃣0️⃣ Real DevOps Kubernetes Workflow

```text id="k8s14"
Developer pushes code → CI/CD pipeline builds Docker image → Push to registry → 
Kubernetes Deployment pulls image → Pods created → Exposed via Service/Ingress → Scaled automatically → Monitored
```

* **Pod** = container unit
* **Deployment** = manages pods & updates
* **Service** = exposes pods
* **Ingress** = external access
* **PVC/PV** = persistent storage

---




Absolutely! Let’s go **deep into Kubernetes commands (`kubectl`)** the way **real DevOps engineers use them in production**. I’ll explain **each command**, its **purpose**, and **examples**, plus **tips for best practices**. This will be your complete **Kubernetes CLI guide**. 🐳➡️☸️

---

# 1️⃣ Basic Cluster Info Commands

### `kubectl version`

* Shows **client & server versions** of Kubernetes.
* Example:

```bash
kubectl version --short
```

Output:

```
Client Version: v1.28.0
Server Version: v1.27.5
```

---

### `kubectl cluster-info`

* Shows **master & cluster info**.
* Example:

```bash
kubectl cluster-info
```

* Useful to **verify cluster is up and running**.

---

### `kubectl config view`

* Shows **current kubeconfig** and context.
* Useful when working with **multiple clusters**.

```bash
kubectl config view
kubectl config current-context
kubectl config use-context dev-cluster
```

---

# 2️⃣ Working with Pods

### `kubectl get pods`

* Lists pods in the **current namespace**.
* Example:

```bash
kubectl get pods
kubectl get pods -n dev
kubectl get pods -o wide
```

* `-o wide` → shows node and IP info

---

### `kubectl describe pod <pod-name>`

* Detailed information about **a pod’s status, events, containers**.
* Example:

```bash
kubectl describe pod myapp-pod
```

* Useful for **debugging pod issues**.

---

### `kubectl logs <pod-name>`

* Shows logs from a pod.
* For multi-container pods:

```bash
kubectl logs <pod-name> -c <container-name>
```

* Example:

```bash
kubectl logs myapp-pod
kubectl logs myapp-pod -c nginx
```

---

### `kubectl exec -it <pod-name> -- /bin/sh`

* Opens a **shell inside the container**.
* Useful for **debugging runtime issues**.

```bash
kubectl exec -it myapp-pod -- /bin/sh
```

---

### `kubectl delete pod <pod-name>`

* Deletes a pod (it may be **recreated by Deployment/ReplicaSet**).

---

# 3️⃣ Deployments & ReplicaSets

### `kubectl get deployments`

* Lists all deployments in namespace:

```bash
kubectl get deployments
kubectl get deployments -n prod
```

---

### `kubectl describe deployment <deployment-name>`

* Shows detailed deployment info:

```bash
kubectl describe deployment myapp-deploy
```

* Shows pods, strategy, replica counts, events.

---

### `kubectl scale deployment <deployment-name> --replicas=<num>`

* Scale deployment manually:

```bash
kubectl scale deployment myapp-deploy --replicas=5
```

* Automatically handled with HPA in production.

---

### `kubectl rollout status deployment <deployment-name>`

* Check **progress of rolling update**:

```bash
kubectl rollout status deployment myapp-deploy
```

---

### `kubectl rollout undo deployment <deployment-name>`

* Rollback to previous deployment version:

```bash
kubectl rollout undo deployment myapp-deploy
```

---

# 4️⃣ Services

### `kubectl get services`

* List all services:

```bash
kubectl get svc
kubectl get svc -n staging
```

---

### `kubectl describe service <service-name>`

* Shows **service type, endpoints, ports, and selector**:

```bash
kubectl describe svc myapp-service
```

---

# 5️⃣ Namespaces

### `kubectl get namespaces`

* Lists all namespaces:

```bash
kubectl get ns
```

---

### `kubectl create namespace <name>`

```bash
kubectl create namespace dev
```

---

### `kubectl delete namespace <name>`

* Deletes **all resources inside namespace**:

```bash
kubectl delete namespace dev
```

---

# 6️⃣ ConfigMaps & Secrets

### ConfigMaps

```bash
kubectl get configmaps
kubectl describe configmap <configmap-name>
kubectl create configmap myconfig --from-literal=key=value
kubectl apply -f configmap.yaml
```

### Secrets

```bash
kubectl get secrets
kubectl describe secret <secret-name>
kubectl create secret generic db-secret --from-literal=password=1234
kubectl apply -f secret.yaml
```

---

# 7️⃣ Persistent Volumes & PVCs

### Persistent Volumes (PV)

```bash
kubectl get pv
kubectl describe pv <pv-name>
```

### Persistent Volume Claims (PVC)

```bash
kubectl get pvc
kubectl describe pvc <pvc-name>
```

---

# 8️⃣ Apply & Delete Resources

### Apply (create/update)

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f .
```

* Idempotent → safe to run multiple times

---

### Delete

```bash
kubectl delete -f deployment.yaml
kubectl delete pod myapp-pod
```

---

# 9️⃣ Scaling & Autoscaling

### Manual scaling

```bash
kubectl scale deployment myapp-deploy --replicas=3
```

### Horizontal Pod Autoscaler (HPA)

```bash
kubectl autoscale deployment myapp-deploy --cpu-percent=50 --min=2 --max=10
kubectl get hpa
```

---

# 🔟 Networking & Port Forwarding

### Port Forward

* Access a pod locally without exposing via Service:

```bash
kubectl port-forward pod/myapp-pod 8080:80
```

* Access **[http://localhost:8080](http://localhost:8080)** → pod’s port 80

---

### Exec Networking

* Check connectivity inside pod:

```bash
kubectl exec -it myapp-pod -- ping google.com
kubectl exec -it myapp-pod -- curl http://another-service
```

---

# 1️⃣1️⃣ Get Everything Together

### List All Resources

```bash
kubectl get all
kubectl get all -n prod
```

* Shows pods, deployments, services, replica sets, etc.

---

# 1️⃣2️⃣ Top Commands for DevOps Production Use

| Command                             | Usage                    |
| ----------------------------------- | ------------------------ |
| `kubectl get pods`                  | Check pod status         |
| `kubectl describe pod <pod>`        | Debug pod issues         |
| `kubectl logs <pod>`                | View logs                |
| `kubectl exec -it <pod> -- /bin/sh` | Access container shell   |
| `kubectl get deployments`           | Check deployments        |
| `kubectl rollout status deployment` | Monitor rolling updates  |
| `kubectl get svc`                   | Check services/endpoints |
| `kubectl get namespaces`            | Multi-team envs          |
| `kubectl apply -f <file>`           | Deploy/update resources  |
| `kubectl delete -f <file>`          | Remove resources         |
| `kubectl scale deployment`          | Manual scaling           |
| `kubectl autoscale deployment`      | HPA autoscaling          |
| `kubectl port-forward`              | Debug/test networking    |

---

# ✅ Best Practices for DevOps Engineers

* Use **namespaces** to separate environments
* Use **labels & selectors** for resource management
* Always **check pod logs** for errors in production
* Automate deployments with **CI/CD pipelines**
* Monitor cluster with **Prometheus & Grafana**

---


Perfect! Let’s create a **visual Kubernetes cheat sheet** that summarizes **core Kubernetes objects** and maps them to **the most important `kubectl` commands**. This is exactly what DevOps engineers use for quick reference. 🐳☸️

I’ll structure it visually, object by object, with examples and commands.

---

![Image](https://ik.imagekit.io/upgrad1/abroad-images/imageCompo/images/jjOJMXC5.png?pr-true=)

![Image](https://cdn.prod.website-files.com/635e4ccf77408db6bd802ae6/684851ab3a46b6e3b87edb27_AD_4nXc0RtB_oDIgvU9zrnv2E_1kADLzpgJ9FbLQYWF5t9FeongzuMMPCBAPzcOTSHNXWFotksXN9UI6_t_YQO16k_4a-Q2aCaFcSS7L0arQ7ASxZEccUld9i2tidwhyw9cRgghF6p4w.jpeg)

---

# 🟢 Kubernetes Cheat Sheet – Core Objects & Commands

## 1️⃣ Pods

* **Definition:** Smallest deployable unit in Kubernetes.
* **Contains:** 1 or more containers, shared storage/network.
* **Use case:** Run single instance of an app/container.

**Common `kubectl` commands:**

| Command                             | Description                 |
| ----------------------------------- | --------------------------- |
| `kubectl get pods`                  | List pods                   |
| `kubectl describe pod <pod>`        | Show detailed info & events |
| `kubectl logs <pod>`                | View container logs         |
| `kubectl exec -it <pod> -- /bin/sh` | Open shell inside pod       |
| `kubectl delete pod <pod>`          | Delete pod                  |

---

## 2️⃣ ReplicaSets

* **Definition:** Ensures a specified **number of pod replicas** are running.
* **Use case:** Self-healing – recreates pods if they die.

**Commands:**

| Command                                   | Description               |
| ----------------------------------------- | ------------------------- |
| `kubectl get rs`                          | List ReplicaSets          |
| `kubectl describe rs <rs-name>`           | View detailed info        |
| `kubectl scale rs <rs-name> --replicas=3` | Scale ReplicaSet manually |

---

## 3️⃣ Deployments

* **Definition:** Manages ReplicaSets & enables **rolling updates/rollbacks**.
* **Use case:** Production-level app management, version updates.

**Commands:**

| Command                                              | Description                  |
| ---------------------------------------------------- | ---------------------------- |
| `kubectl get deployments`                            | List deployments             |
| `kubectl describe deployment <deployment>`           | Detailed info                |
| `kubectl rollout status deployment <deployment>`     | Check update progress        |
| `kubectl rollout undo deployment <deployment>`       | Rollback to previous version |
| `kubectl scale deployment <deployment> --replicas=5` | Manual scaling               |

---

## 4️⃣ Services

* **Definition:** Expose pods internally or externally.
* **Types:** `ClusterIP` (internal), `NodePort` (external), `LoadBalancer` (cloud).

**Commands:**

| Command                                                 | Description                |
| ------------------------------------------------------- | -------------------------- |
| `kubectl get svc`                                       | List services              |
| `kubectl describe svc <service>`                        | Show service details       |
| `kubectl expose pod <pod> --port=80 --target-port=8080` | Create a service for a pod |

---

## 5️⃣ Namespaces

* **Definition:** Logical separation of resources inside a cluster.
* **Use case:** Multi-team, dev/staging/prod separation.

**Commands:**

| Command                                                   | Description              |
| --------------------------------------------------------- | ------------------------ |
| `kubectl get namespaces`                                  | List namespaces          |
| `kubectl create namespace <name>`                         | Create namespace         |
| `kubectl delete namespace <name>`                         | Delete namespace         |
| `kubectl config set-context --current --namespace=<name>` | Switch default namespace |

---

## 6️⃣ Persistent Volumes (PV) & Persistent Volume Claims (PVC)

* **PV:** Physical storage resource in cluster
* **PVC:** Pod request for storage

**Commands:**

| Command                      | Description             |
| ---------------------------- | ----------------------- |
| `kubectl get pv`             | List persistent volumes |
| `kubectl describe pv <pv>`   | Detailed PV info        |
| `kubectl get pvc`            | List PVCs               |
| `kubectl describe pvc <pvc>` | Detailed PVC info       |
| `kubectl apply -f pvc.yaml`  | Create a PVC            |

---

## 7️⃣ Common `kubectl` Utility Commands

| Command                                              | Description                         |
| ---------------------------------------------------- | ----------------------------------- |
| `kubectl get all`                                    | List all resources in namespace     |
| `kubectl apply -f <file>`                            | Create/update resources             |
| `kubectl delete -f <file>`                           | Delete resources                    |
| `kubectl port-forward <pod> <local-port>:<pod-port>` | Test pod connectivity locally       |
| `kubectl top pods`                                   | Resource usage per pod (CPU/Memory) |
| `kubectl exec -it <pod> -- <command>`                | Run commands inside pod             |

---

### 🔹 Quick Visual Hierarchy

```text id="k8s_hierarchy"
Cluster
 ├── Namespace
 │    ├── Deployment
 │    │    ├── ReplicaSet
 │    │    │    ├── Pods
 │    │    │    │    ├── Containers
 │    │    │    │    └── Volumes (PV/PVC)
 │    │    └── Services (ClusterIP, NodePort, LoadBalancer)
 │    └── ConfigMaps / Secrets
```

* Shows how **Pods, ReplicaSets, Deployments, Services, Namespaces, and PV/PVC** are connected.
* All objects interact in **DevOps workflows** for production-grade applications.

---








Absolutely! Let’s dive into **Helm**, the Kubernetes package manager, which is a **must-know tool for DevOps engineers** managing production-grade K8s deployments. 🚀☸️

---

# 1️⃣ What is Helm?

**Helm** is like **apt/yum for Kubernetes**:

* It **packages Kubernetes manifests** (Deployments, Services, ConfigMaps, etc.) into a reusable format called a **chart**.
* Helps **deploy, upgrade, and rollback applications** in Kubernetes with a single command.
* Reduces complexity when managing multiple K8s resources.

Think of it as:

```text
Without Helm: kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                kubectl apply -f configmap.yaml
                ...
With Helm: helm install myapp ./myapp-chart
```

---

# 2️⃣ Key Helm Concepts

| Term           | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| **Chart**      | A package of Kubernetes manifests (like an application template) |
| **Release**    | A deployed instance of a chart                                   |
| **Repository** | Collection of Helm charts (like Docker registry)                 |
| **Values**     | Configuration file (`values.yaml`) to customize deployments      |

---

# 3️⃣ Helm Architecture

* Helm has **2 main components**:

1️⃣ **Helm CLI** – Installed on your local machine, interacts with K8s cluster.
2️⃣ **Helm Tiller (Helm v2 only)** – Used to manage releases inside cluster (removed in Helm v3).

* Helm v3 **does not require Tiller** → safer for production.

---

# 4️⃣ Installing Helm

```bash
# MacOS (Homebrew)
brew install helm

# Linux
curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Verify
helm version
```

---

# 5️⃣ Helm Repositories

* Official Helm repo:

```bash
helm repo add stable https://charts.helm.sh/stable
helm repo update
```

* Search charts:

```bash
helm search repo nginx
```

* Example: Deploy **NGINX using Helm**:

```bash
helm install my-nginx stable/nginx-ingress
```

---

# 6️⃣ Helm Charts Structure

Typical Helm chart directory:

```
myapp-chart/
├── Chart.yaml        # Chart metadata (name, version)
├── values.yaml       # Default configuration values
├── templates/        # Kubernetes manifest templates
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
└── charts/           # Optional sub-charts / dependencies
```

* **Chart.yaml:** Defines name, version, description
* **values.yaml:** Default settings that can be overridden
* **templates/**: Use Go templating to create dynamic K8s manifests

---

# 7️⃣ Helm Commands (DevOps Workflow)

| Command                              | Description                                 |
| ------------------------------------ | ------------------------------------------- |
| `helm repo add <name> <url>`         | Add Helm repository                         |
| `helm repo update`                   | Update chart information                    |
| `helm search repo <keyword>`         | Search for charts                           |
| `helm install <release> <chart>`     | Install a chart as a release                |
| `helm upgrade <release> <chart>`     | Upgrade a release                           |
| `helm rollback <release> <revision>` | Rollback release to previous version        |
| `helm list`                          | List installed releases                     |
| `helm uninstall <release>`           | Remove a release                            |
| `helm template <chart>`              | Render manifests locally without installing |

---

# 8️⃣ Customizing Deployments with `values.yaml`

* Example: Change replicas and image:

```yaml
# values.yaml
replicaCount: 3
image:
  repository: myapp
  tag: 1.0.0
service:
  type: LoadBalancer
  port: 80
```

* Install with custom values:

```bash
helm install myapp ./myapp-chart -f values.yaml
```

* Override single value inline:

```bash
helm install myapp ./myapp-chart --set replicaCount=5
```

---

# 9️⃣ Helm Upgrade & Rollback

* Upgrade app safely:

```bash
helm upgrade myapp ./myapp-chart -f values.yaml
```

* Rollback if upgrade fails:

```bash
helm rollback myapp 1
```

* Helm keeps **release history**, so production rollbacks are easy.

---

# 🔹 Benefits of Helm for DevOps

1. **Reusability:** Package K8s apps into charts
2. **Consistency:** Deploy apps with same configuration across environments
3. **Versioning:** Keep track of releases, easy rollbacks
4. **Automation:** Integrate into CI/CD pipelines (Jenkins, GitHub Actions)
5. **Simplifies dependencies:** Charts can include sub-charts (databases, caches, etc.)

---

# 🔟 Real DevOps Workflow with Helm

```text
Developer commits code → CI/CD builds Docker image → Push to registry → 
Helm chart deploys app to Kubernetes → Helm upgrade for new version → Rollback if necessary
```

* Helm makes **multi-component apps easy to deploy** with a single command.
* Ideal for production, multi-environment deployments.

---

✅ Key Takeaways:

* Helm = **package manager for Kubernetes**
* Charts = reusable templates
* Releases = deployed instances
* Values.yaml = configuration
* Helm workflow = **install → upgrade → rollback → uninstall**

---




Absolutely! Monitoring and logging are **cornerstones of production-grade DevOps**. They help you **observe your Kubernetes/Docker applications, detect issues, and ensure reliability**. Let’s break it down step by step with **Prometheus, Grafana, and ELK Stack**. 📊🖥️

---

# 1️⃣ Why Monitoring & Logging?

| Purpose               | Examples                                                     |
| --------------------- | ------------------------------------------------------------ |
| **Monitoring**        | Keep track of CPU, memory, disk usage, application metrics   |
| **Alerting**          | Notify teams if something goes wrong (high CPU, failed pods) |
| **Logging**           | Record application events, errors, audit trails              |
| **Debugging**         | Analyze logs/metrics to fix issues quickly                   |
| **Capacity Planning** | Understand usage patterns and scale accordingly              |

> Without monitoring & logging, production systems become a “black box.”

---

# 2️⃣ Monitoring with **Prometheus**

**Prometheus** is a **time-series database + monitoring system** for metrics.

* Collects metrics from **Kubernetes, Docker, and apps**.
* Pulls metrics from **/metrics endpoint** (Prometheus exporters).
* Can trigger **alerts** via **Alertmanager**.

### How it works:

```text id="prometheus_flow"
Kubernetes / Docker → Exporters → Prometheus scrapes metrics → Stores metrics → Grafana visualizes → Alertmanager sends notifications
```

### Prometheus Key Concepts:

| Term             | Description                                                                       |
| ---------------- | --------------------------------------------------------------------------------- |
| **Target**       | Application or service exposing metrics                                           |
| **Exporter**     | Converts app/service metrics to Prometheus format (e.g., Node Exporter, cAdvisor) |
| **Scrape**       | Prometheus pulling metrics at intervals                                           |
| **Alertmanager** | Handles alert notifications via Slack, Email, PagerDuty                           |

### Example: Metrics for Kubernetes Pod

```text id="prometheus_metrics_example"
pod_cpu_usage_seconds_total{pod="myapp-pod"}
pod_memory_usage_bytes{pod="myapp-pod"}
```

---

# 3️⃣ Visualization with **Grafana**

**Grafana** is a **visualization tool** for metrics (from Prometheus, InfluxDB, etc.).

* Create **dashboards** for metrics like CPU, memory, response times.
* Set **threshold alerts** to notify on anomalies.
* Works for **Kubernetes, Docker, and cloud apps**.

### Example Dashboards:

* Cluster CPU/Memory Usage
* Pod Restarts / Status
* Application Latency / Errors
* Node Health

---

# 4️⃣ Logging with **ELK Stack**

**ELK = Elasticsearch + Logstash + Kibana**

| Component         | Role                                                  |
| ----------------- | ----------------------------------------------------- |
| **Elasticsearch** | Stores and indexes logs (searchable)                  |
| **Logstash**      | Collects, transforms, and sends logs to Elasticsearch |
| **Kibana**        | Visualizes logs and creates dashboards                |

### Optional: **Beats** (lightweight log collectors):

* **Filebeat** → reads container or application logs
* **Metricbeat** → collects metrics like CPU/memory

### Example: Logs from Kubernetes Pod

```text id="elk_example"
2026-03-07 14:23:12 ERROR myapp-pod: Connection timeout to DB
2026-03-07 14:23:15 INFO myapp-pod: Request served in 120ms
```

* Search in Kibana: `pod:myapp-pod AND level:ERROR` → shows all errors from this pod

---

# 5️⃣ DevOps Production Workflow Example

```text id="monitoring_flow"
Kubernetes Cluster:
  - Pods expose metrics (/metrics)
  - cAdvisor & Node Exporter → system metrics

Prometheus:
  - Scrapes metrics at intervals
  - Stores metrics in time-series database
  - Triggers alerts via Alertmanager

Grafana:
  - Connects to Prometheus
  - Visual dashboards for monitoring CPU, memory, latency, errors

ELK Stack:
  - Logs collected from pods/containers
  - Logstash parses logs
  - Elasticsearch stores them
  - Kibana visualizes & searches logs
```

**Outcome:**

* Real-time monitoring + alerting
* Historical analysis
* Quick debugging

---

# 6️⃣ Key Commands / Setup (Simplified)

### Prometheus (Kubernetes)

```bash id="prometheus_k8s"
kubectl create namespace monitoring
kubectl apply -f prometheus-deployment.yaml
kubectl get pods -n monitoring
kubectl port-forward svc/prometheus 9090:9090 -n monitoring
```

### Grafana

```bash id="grafana_k8s"
kubectl apply -f grafana-deployment.yaml
kubectl port-forward svc/grafana 3000:3000 -n monitoring
```

### ELK (ECK Operator for Kubernetes)

```bash id="elk_k8s"
kubectl apply -f elasticsearch.yaml
kubectl apply -f kibana.yaml
kubectl port-forward svc/kibana 5601:5601
```

* View logs → Kibana UI
* Search, filter, and create dashboards

---

# 7️⃣ DevOps Best Practices for Monitoring & Logging

✅ Use **Prometheus + Grafana** for metrics monitoring
✅ Use **ELK Stack** for logs
✅ Set **alerts** for critical events (CPU spikes, pod restarts, errors)
✅ Separate **metrics and logs namespaces**
✅ Automate deployment using **Helm charts** for Prometheus/Grafana/ELK
✅ Use **labels and annotations** in Kubernetes for filtering metrics/logs

---

# 🔹 Summary

| Tool           | Purpose            | Kubernetes Use Case                      |
| -------------- | ------------------ | ---------------------------------------- |
| **Prometheus** | Metrics collection | Pod CPU/memory, app metrics              |
| **Grafana**    | Visualization      | Dashboards, alerts                       |
| **ELK Stack**  | Logging            | Container logs, error tracking, auditing |

* Together, these tools provide **full observability** in Kubernetes/Docker production environments.
* Enables **DevOps teams to detect, alert, and debug** quickly.

---





Absolutely! Let’s dive into **production deployment patterns** like **Blue/Green** and **Canary deployments**, which are essential for **DevOps engineers** to deploy applications safely and reliably. 🚀☸️

---

# 1️⃣ Why Deployment Patterns Matter

In production, we want to:

* Minimize downtime
* Reduce risk of breaking the application
* Test new versions with real users gradually
* Rollback safely if something goes wrong

**Without patterns:** Directly updating a Deployment can **break users’ experience**.

---

# 2️⃣ Blue/Green Deployment

**Concept:** Maintain **two identical environments**:

* **Blue** → Current production version
* **Green** → New version to deploy

**Workflow:**

1. Users are using **Blue** (live version).
2. Deploy new version to **Green** environment.
3. Test Green internally (smoke tests, QA).
4. Switch traffic from Blue → Green.
5. If anything fails → rollback to Blue.

**Diagram:**

```text id="blue_green"
Traffic
   │
   ├──> Blue (current)
   └──> Green (new)
```

**Kubernetes Implementation:**

* Use **two separate Deployments** or **Namespaces**.
* Use **Service** to route traffic:

```yaml id="blue_green_service"
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp-green  # switch from blue → green
  ports:
    - port: 80
      targetPort: 8080
```

**Pros:**

* Zero downtime
* Easy rollback (switch Service back to Blue)

**Cons:**

* Requires **double resources** (Blue + Green running simultaneously)

---

# 3️⃣ Canary Deployment

**Concept:** Release new version **gradually** to a subset of users.

**Workflow:**

1. Deploy new version as a **small percentage** of pods (Canary pods).
2. Monitor metrics (CPU, errors, response time).
3. If healthy → gradually increase traffic.
4. If unhealthy → rollback Canary pods.

**Diagram:**

```text id="canary"
Users
 ├─ 90% → Blue (stable)
 └─ 10% → Green (canary)
```

**Kubernetes Implementation:**

* Use **Deployment with multiple replicas**
* Use **labels and selectors** + **Ingress/Service routing**

Example:

```yaml id="canary_deployment"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-canary
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
      version: canary
  template:
    metadata:
      labels:
        app: myapp
        version: canary
    spec:
      containers:
      - name: myapp
        image: myapp:2.0
```

* Service can route **10% traffic to canary** using tools like **Istio, Linkerd, or NGINX Ingress**.

**Pros:**

* Low-risk deployment
* Monitor real user behavior before full rollout

**Cons:**

* More complex setup
* Requires **observability tools** (Prometheus, Grafana, ELK)

---

# 4️⃣ Comparing Blue/Green vs Canary

| Feature        | Blue/Green                   | Canary                             |
| -------------- | ---------------------------- | ---------------------------------- |
| Downtime       | 0                            | 0 (if done properly)               |
| Resource Usage | High (two full environments) | Low (subset of pods)               |
| Rollback       | Switch service back          | Delete canary pods                 |
| Risk           | Low                          | Very low (gradual rollout)         |
| Observability  | Optional                     | Essential (monitor metrics & logs) |

---

# 5️⃣ CI/CD Integration

**How DevOps uses these patterns:**

1. Developer pushes code → CI/CD pipeline builds Docker image.
2. Push image to registry (ECR/GCR/ACR).
3. Pipeline deploys image:

* **Blue/Green:** Helm or `kubectl apply` to new namespace/deployment. Switch Service.
* **Canary:** Update Deployment with subset replicas, route portion of traffic.

4. Monitor metrics/logs (Prometheus, Grafana, ELK).
5. Promote new version to 100% traffic or rollback.

**Visual Workflow:**

```text id="ci_cd_canary_bluegreen"
Code Commit
     ↓
Docker Build → Push Registry
     ↓
CI/CD Pipeline Deploy
     ↓
Blue/Green or Canary Deployment
     ↓
Monitor Metrics & Logs
     ↓
Switch/Promote/Rollback
```

---

# 6️⃣ Best Practices for Production Deployments

✅ Always use **immutable Docker images** (tagged, not `latest`).
✅ Use **Helm** or **Kustomize** to manage deployments.
✅ Monitor **CPU, memory, errors, latency** during rollout.
✅ Use **feature flags** for selective exposure.
✅ Automate **rollback strategies** in CI/CD.
✅ Document deployment process for team knowledge.

---

# ✅ Key Takeaways

* **Blue/Green:** full duplicate environment, switch traffic, easy rollback, higher cost.
* **Canary:** gradual rollout to subset of users, low-risk, requires monitoring.
* Both patterns are **essential for production-grade DevOps deployments**.

---






































Great choice starting with **Docker** in DevOps. Interviewers often ask **scenario-based questions** to check whether you really understand containers, not just commands. Below are **some tricky/situation-based Docker questions with clear answers**. 🚀

---

## 1. Container Keeps Restarting

**Question:**
You deployed a container using Docker, but it keeps restarting continuously. How would you debug it?

**Answer:**

Steps to troubleshoot:

1. Check container status

```bash
docker ps -a
```

2. View logs

```bash
docker logs <container_id>
```

3. Inspect container for detailed configuration

```bash
docker inspect <container_id>
```

4. Run container interactively to debug

```bash
docker run -it <image_name> /bin/bash
```

5. Check restart policy

```bash
docker inspect --format='{{.HostConfig.RestartPolicy.Name}}' <container_id>
```

**Common causes**

* Application crash
* Wrong command in `CMD` or `ENTRYPOINT`
* Missing environment variables
* Port conflict

---

## 2. Docker Container Cannot Connect to Database

**Question:**
Your application container cannot connect to a database container running on the same host.

**Answer:**

Check these things:

1. Verify containers are running

```bash
docker ps
```

2. Ensure both containers are in the **same network**

```bash
docker network ls
docker network inspect <network_name>
```

3. Use container name instead of `localhost`

Example:

```
DB_HOST=mysql_container
```

4. Test connectivity

```bash
docker exec -it app_container ping mysql_container
```

**Key Concept:**
Containers communicate using **Docker network and container name as hostname**.

---

## 3. Docker Image Size is Too Large

**Question:**
Your Docker image is 1.5GB and builds slowly. How do you reduce its size?

**Answer:**

Techniques:

1. Use smaller base image

Instead of:

```dockerfile
FROM ubuntu
```

Use:

```dockerfile
FROM alpine
```

2. Use **multi-stage builds**

```dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install

FROM node:18-alpine
COPY --from=builder /app /app
```

3. Combine RUN commands

Bad:

```dockerfile
RUN apt update
RUN apt install curl
```

Good:

```dockerfile
RUN apt update && apt install -y curl
```

4. Use `.dockerignore`

Example:

```
node_modules
.git
logs
```

---

## 4. Changes in Code Not Reflecting in Container

**Question:**
You updated your application code but changes are not reflected in the running container.

**Answer:**

Possible reasons:

1. You didn't rebuild the image

```bash
docker build -t myapp .
```

2. Container still using old image

```bash
docker stop <container>
docker rm <container>
docker run myapp
```

3. If using volumes, check mount path

```bash
docker run -v $(pwd):/app myapp
```

---

## 5. Data Lost After Container Restart

**Question:**
Your database container loses data after restart. Why?

**Answer:**

Because containers are **ephemeral**.

Solution: Use **Docker volumes**.

Example:

```bash
docker run -d \
-v mysql_data:/var/lib/mysql \
mysql
```

Create volume manually:

```bash
docker volume create mysql_data
```

Now data persists even if container is removed.

---

## 6. Port Not Accessible from Host

**Question:**
Your containerized web app runs on port 3000 but you cannot access it from the browser.

**Answer:**

Check port mapping:

```bash
docker ps
```

Example correct mapping:

```bash
docker run -p 3000:3000 myapp
```

Also verify app listens on:

```
0.0.0.0
```

not

```
localhost
```

Inside container.

---

## 7. Docker Build is Very Slow

**Question:**
Your Docker builds take 10 minutes every time. How do you optimize it?

**Answer:**

Use **Docker layer caching**.

Bad Dockerfile:

```dockerfile
COPY . .
RUN npm install
```

Better:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

Now dependencies install only when `package.json` changes.

---

## 8. Need to Run Multiple Containers Together

**Question:**
Your application has:

* frontend
* backend
* database

How do you manage them?

**Answer:**

Use **Docker Compose**.

Example `docker-compose.yml`

```yaml
version: "3"

services:
  web:
    build: .
    ports:
      - "3000:3000"

  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
```

Run:

```bash
docker-compose up
```

---

## 9. Container Consuming High CPU

**Question:**
A Docker container is consuming too much CPU. How do you limit it?

**Answer:**

Run container with resource limits.

Example:

```bash
docker run --cpus="1.5" myapp
```

Memory limit:

```bash
docker run -m 512m myapp
```

---

## 10. Difference Between CMD and ENTRYPOINT

**Question:**
What happens if both CMD and ENTRYPOINT exist in a Dockerfile?

**Answer:**

Example:

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Execution becomes:

```bash
python app.py
```

Key difference:

| CMD               | ENTRYPOINT         |
| ----------------- | ------------------ |
| Default command   | Main executable    |
| Can be overridden | Harder to override |

---

💡 **Pro Tip (Interview):**
Interviewers often test these **core Docker concepts**:

* Container vs Image
* Volumes
* Networking
* Dockerfile optimization
* Multi-stage builds
* Debugging containers
* Docker Compose

---





Here are **20 Advanced Docker Interview Questions** that are commonly asked in **real DevOps interviews**. These focus on **architecture, troubleshooting, performance, and production usage** rather than basic commands. 🚀

---

# 20 Advanced Docker Interview Questions (Real DevOps Interviews)

---

## 1. What is the difference between Docker Image and Container?

**Answer**

| Docker Image              | Docker Container          |
| ------------------------- | ------------------------- |
| Read-only template        | Running instance of image |
| Used to create containers | Executes the application  |
| Immutable                 | Can change during runtime |

Example:

```
Image → blueprint
Container → running machine
```

---

## 2. What happens when you run `docker run`?

**Answer**

`docker run` performs multiple steps:

1. Pulls image if not present
2. Creates container
3. Creates writable container layer
4. Configures networking
5. Starts container process

Internally it executes:

```
docker create
docker start
```

---

## 3. Explain Docker layered filesystem.

**Answer**

Docker images are built using **layers**.

Example Dockerfile:

```dockerfile
FROM ubuntu
RUN apt update
RUN apt install nginx
COPY . /app
```

Layers created:

```
Layer 1 → Ubuntu base
Layer 2 → apt update
Layer 3 → nginx install
Layer 4 → copy files
```

Benefits:

* Faster builds
* Layer caching
* Reusability
* Smaller downloads

---

## 4. What is the difference between COPY and ADD?

**Answer**

| COPY              | ADD                        |
| ----------------- | -------------------------- |
| Copies files only | Copies + extracts archives |
| Preferred command | Has extra features         |
| Simple behavior   | Can download URLs          |

Best practice:

```
Use COPY unless ADD features are needed
```

---

## 5. How do you persist data in Docker?

**Answer**

Use **Volumes or Bind Mounts**.

Example volume:

```bash
docker run -v mysql_data:/var/lib/mysql mysql
```

Example bind mount:

```bash
docker run -v /host/data:/container/data nginx
```

Difference:

| Volume            | Bind Mount      |
| ----------------- | --------------- |
| Managed by Docker | Host filesystem |
| Safer             | Flexible        |

---

## 6. What is Docker networking?

**Answer**

Docker allows containers to communicate using networks.

Types:

| Network Type | Use Case               |
| ------------ | ---------------------- |
| Bridge       | Default for containers |
| Host         | Uses host network      |
| None         | No networking          |
| Overlay      | Multi-host networking  |
| Macvlan      | Container gets real IP |

Example:

```
docker network create mynetwork
```

---

## 7. What is the difference between Bridge and Host network?

**Answer**

| Bridge                     | Host                |
| -------------------------- | ------------------- |
| Default network            | Shares host network |
| Isolated container network | No isolation        |
| Requires port mapping      | No port mapping     |

Example:

```
docker run --network host nginx
```

---

## 8. What is Docker Compose?

**Answer**

Docker Compose is used to **manage multi-container applications**.

Example stack:

* frontend
* backend
* database

Example file:

```yaml
version: "3"

services:
  web:
    build: .
    ports:
      - "3000:3000"

  db:
    image: mysql
```

Run:

```
docker-compose up
```

---

## 9. What is Multi-stage Build?

**Answer**

Used to **reduce image size**.

Example:

```dockerfile
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install

FROM node:18-alpine
COPY --from=build /app /app
```

Benefits:

* Smaller images
* Better security
* Faster deployments

---

## 10. How does Docker caching work?

**Answer**

Docker reuses layers if instructions don't change.

Example:

Bad:

```dockerfile
COPY . .
RUN npm install
```

Better:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

Now dependency layer is cached.

---

## 11. What is Docker Registry?

**Answer**

A registry stores Docker images.

Examples:

* Docker Hub
* AWS ECR
* GitHub Container Registry
* Google Container Registry

Push image example:

```
docker push username/myapp:latest
```

---

## 12. What is the difference between Dockerfile CMD and ENTRYPOINT?

**Answer**

| CMD               | ENTRYPOINT      |
| ----------------- | --------------- |
| Default command   | Main executable |
| Can be overridden | Usually fixed   |

Example:

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Runs:

```
python app.py
```

---

## 13. How do you debug a running container?

**Answer**

Common commands:

Check logs:

```
docker logs container_id
```

Access container:

```
docker exec -it container_id bash
```

Inspect container:

```
docker inspect container_id
```

Check resources:

```
docker stats
```

---

## 14. What are Docker Volumes?

**Answer**

Volumes are used to **persist container data**.

Example:

```
docker volume create mydata
```

Use:

```
docker run -v mydata:/data nginx
```

Benefits:

* Data persistence
* Container independence
* Easy backups

---

## 15. What is Docker Swarm?

**Answer**

Docker Swarm is Docker's **native container orchestration tool**.

Features:

* Cluster management
* Load balancing
* Scaling services
* High availability

Initialize swarm:

```
docker swarm init
```

---

## 16. How do you secure Docker containers?

**Answer**

Best practices:

* Use minimal base images (Alpine)
* Avoid running as root
* Use read-only filesystem
* Scan images for vulnerabilities
* Use secrets management

Example:

```
USER appuser
```

---

## 17. What are Docker namespaces?

**Answer**

Namespaces provide **container isolation**.

Types:

* PID
* Network
* Mount
* User
* IPC
* UTS

They isolate:

```
processes
network
filesystem
```

---

## 18. What are Docker cgroups?

**Answer**

Control Groups manage **resource limits**.

Example:

```
docker run -m 512m nginx
```

Limits:

* CPU
* Memory
* Disk IO
* Network

---

## 19. How does Docker achieve container isolation?

**Answer**

Using:

1. **Namespaces** → process isolation
2. **Cgroups** → resource limits
3. **Union filesystem** → layered storage
4. **Capabilities** → restrict privileges

---

## 20. Docker vs Virtual Machines

**Answer**

| Docker           | Virtual Machine |
| ---------------- | --------------- |
| Lightweight      | Heavy           |
| Uses host kernel | Own OS          |
| Faster startup   | Slow startup    |
| Less memory      | More memory     |

Example:

```
VM Boot → minutes
Container Start → seconds
```

---

💡 **Very Important for DevOps Interviews**

Companies often ask **scenario questions like:**

* Container crashes after deployment
* Docker image too large
* Database losing data
* Containers cannot communicate
* Docker build slow
* Port not accessible
* Security vulnerabilities

---









Here are **15 Real Docker Troubleshooting Scenarios** that are frequently asked in **DevOps interviews**. These test whether you can **debug real production issues**, not just run commands. 🚀

---

# 15 Real Docker Troubleshooting Scenarios (DevOps Interviews)

---

# 1. Container Keeps Restarting

### Scenario

Your container keeps restarting continuously.

### How to troubleshoot

Check container status:

```bash
docker ps -a
```

Check logs:

```bash
docker logs <container_id>
```

Inspect container:

```bash
docker inspect <container_id>
```

### Possible causes

* Application crash
* Wrong command in `CMD`
* Missing environment variables
* Port already in use

---

# 2. Cannot Access Application from Browser

### Scenario

You run a container but cannot access it via browser.

### Troubleshooting

Check port mapping:

```bash
docker ps
```

Correct example:

```bash
docker run -p 8080:8080 myapp
```

Verify application listens on:

```
0.0.0.0
```

not

```
localhost
```

---

# 3. Changes in Code Not Reflecting

### Scenario

You updated code but container still runs old code.

### Solution

Rebuild image:

```bash
docker build -t myapp .
```

Restart container:

```bash
docker rm -f myapp_container
docker run myapp
```

Or use volume during development:

```bash
docker run -v $(pwd):/app myapp
```

---

# 4. Docker Image Size Too Large

### Scenario

Image size is 1–2GB causing slow deployments.

### Solutions

Use smaller base image:

```
alpine
```

Use multi-stage builds.

Example:

```dockerfile
FROM node:18 as build
WORKDIR /app
COPY . .
RUN npm install

FROM node:18-alpine
COPY --from=build /app /app
```

---

# 5. Container Cannot Connect to Another Container

### Scenario

Your backend container cannot connect to database container.

### Solution

Ensure both containers use same network:

```bash
docker network create mynetwork
```

Run containers:

```bash
docker run --network mynetwork mysql
docker run --network mynetwork backend
```

Use **container name as hostname**.

---

# 6. Database Data Lost After Restart

### Scenario

Your MySQL container loses data after restart.

### Cause

Containers are **ephemeral**.

### Solution

Use volume:

```bash
docker volume create mysql_data
```

Run container:

```bash
docker run -v mysql_data:/var/lib/mysql mysql
```

---

# 7. Docker Build Very Slow

### Scenario

Docker build takes 10 minutes each time.

### Solution

Use layer caching.

Bad:

```dockerfile
COPY . .
RUN npm install
```

Better:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

---

# 8. Container Exits Immediately

### Scenario

Container starts and exits instantly.

### Cause

Main process finishes.

Example problem:

```dockerfile
CMD ["echo", "Hello"]
```

### Solution

Run long-running process.

Example:

```
nginx
node app.js
```

---

# 9. Permission Denied Error

### Scenario

Application inside container cannot access files.

### Cause

Wrong file permissions.

### Fix

Change ownership:

```bash
chown -R appuser /app
```

Or run container with correct user.

---

# 10. Container Using Too Much CPU

### Scenario

One container consumes entire server CPU.

### Solution

Limit CPU:

```bash
docker run --cpus="1.5" myapp
```

Limit memory:

```bash
docker run -m 512m myapp
```

---

# 11. Disk Space Full Due to Docker

### Scenario

Server disk is full because of Docker.

### Solution

Clean unused resources.

Check usage:

```bash
docker system df
```

Remove unused containers/images:

```bash
docker system prune
```

---

# 12. Cannot Delete Docker Image

### Scenario

You try deleting image but get error.

Example error:

```
image is being used by running container
```

### Solution

Stop container first:

```bash
docker stop container_id
docker rm container_id
docker rmi image_id
```

---

# 13. Environment Variables Not Working

### Scenario

Application not reading environment variables.

### Solution

Pass env variables correctly:

```bash
docker run -e DB_HOST=mysql myapp
```

Or use `.env` file:

```bash
docker run --env-file .env myapp
```

---

# 14. Docker Container Cannot Access Internet

### Scenario

Container cannot download packages.

### Troubleshooting

Check network:

```bash
docker network ls
```

Test connectivity:

```bash
docker exec -it container ping google.com
```

Restart Docker daemon if required.

---

# 15. Application Works Locally But Fails in Docker

### Scenario

App works on host but fails inside container.

### Possible reasons

* Missing dependencies
* Wrong working directory
* File path differences
* Environment variables missing

### Fix

Check logs:

```bash
docker logs container_id
```

Debug inside container:

```bash
docker exec -it container_id bash
```

---

# ⭐ Pro Tip for DevOps Interviews

Interviewers usually check if you know **these Docker debugging tools**:

| Command            | Purpose                      |
| ------------------ | ---------------------------- |
| `docker logs`      | View container logs          |
| `docker exec`      | Run command inside container |
| `docker inspect`   | View container configuration |
| `docker stats`     | Monitor resource usage       |
| `docker system df` | Check disk usage             |

---






































Great 👍 Since you're learning **DevOps**, Kubernetes interviews also focus heavily on **real troubleshooting scenarios** rather than theory. Below are **tricky / situation-based Kubernetes questions with answers** that interviewers often ask freshers and junior DevOps engineers. 🚀

---

# 1. Pod is Running but Application Not Accessible

### Scenario

Your **pod status is Running**, but the application is not accessible from the browser.

### Troubleshooting Steps

Check pod status

```bash
kubectl get pods
```

Check pod logs

```bash
kubectl logs <pod-name>
```

Check service

```bash
kubectl get svc
```

Check endpoints

```bash
kubectl get endpoints
```

### Possible Causes

* Service selector not matching pod labels
* Wrong service type
* Application listening on wrong port
* Network policy blocking traffic

---

# 2. Pod is in CrashLoopBackOff

### Scenario

A pod continuously restarts and shows `CrashLoopBackOff`.

### Troubleshooting

Check logs

```bash
kubectl logs <pod-name>
```

Check events

```bash
kubectl describe pod <pod-name>
```

### Common Causes

* Application crash
* Missing environment variables
* Database not reachable
* Wrong container command

---

# 3. Pod is Pending

### Scenario

Pod stays in `Pending` state for a long time.

### Troubleshooting

Check pod details

```bash
kubectl describe pod <pod-name>
```

### Possible Reasons

* No node has enough CPU or memory
* Node selector mismatch
* Taints and tolerations issue
* Persistent volume not available

---

# 4. Service Not Routing Traffic to Pods

### Scenario

You created a service but traffic isn't reaching pods.

### Troubleshooting

Check labels on pod

```bash
kubectl get pods --show-labels
```

Check service selector

```bash
kubectl describe svc <service-name>
```

### Fix

Ensure labels match:

```
Pod label: app=frontend
Service selector: app=frontend
```

---

# 5. Pod Cannot Connect to Database

### Scenario

Backend pod cannot connect to database pod.

### Troubleshooting

Check service name

```bash
kubectl get svc
```

Check DNS inside pod

```bash
kubectl exec -it <pod-name> -- nslookup mysql
```

### Best Practice

Use service name as hostname

```
mysql.default.svc.cluster.local
```

or simply

```
mysql
```

---

# 6. Node is Not Ready

### Scenario

A node shows `NotReady`.

### Troubleshooting

Check nodes

```bash
kubectl get nodes
```

Describe node

```bash
kubectl describe node <node-name>
```

Check kubelet service on node

```
systemctl status kubelet
```

### Possible Causes

* kubelet stopped
* networking issue
* disk pressure
* memory pressure

---

# 7. ConfigMap Changes Not Reflecting

### Scenario

You updated a ConfigMap but the application still uses old config.

### Reason

Pods do not automatically restart when ConfigMap changes.

### Solution

Restart deployment

```bash
kubectl rollout restart deployment <deployment-name>
```

---

# 8. Pod Using Too Much Memory

### Scenario

Pod consumes too much memory causing node issues.

### Solution

Set resource limits.

Example:

```yaml
resources:
  requests:
    memory: "256Mi"
  limits:
    memory: "512Mi"
```

Check usage

```bash
kubectl top pod
```

---

# 9. Deployment Not Updating Pods

### Scenario

You updated deployment image but pods still run old version.

### Troubleshooting

Check rollout status

```bash
kubectl rollout status deployment <deployment-name>
```

Check deployment

```bash
kubectl describe deployment <deployment-name>
```

Force update

```bash
kubectl set image deployment/myapp app=myimage:v2
```

---

# 10. Pod Cannot Pull Image

### Scenario

Pod status shows `ImagePullBackOff`.

### Troubleshooting

Check pod events

```bash
kubectl describe pod <pod-name>
```

### Causes

* Wrong image name
* Image not in registry
* Authentication issue
* Private registry access missing

---

# 11. Persistent Volume Not Mounting

### Scenario

Pod fails because volume cannot mount.

### Troubleshooting

Check PVC

```bash
kubectl get pvc
```

Check PV

```bash
kubectl get pv
```

Check pod events

```bash
kubectl describe pod <pod-name>
```

---

# 12. Pods Not Distributed Across Nodes

### Scenario

All pods run on the same node.

### Solution

Use **pod anti-affinity**.

Example:

```yaml
affinity:
  podAntiAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
```

This spreads pods across nodes.

---

# 13. Rolling Update Failed

### Scenario

Deployment update fails and application goes down.

### Solution

Rollback deployment.

```bash
kubectl rollout undo deployment <deployment-name>
```

Check rollout history

```bash
kubectl rollout history deployment <deployment-name>
```

---

# 14. Need to Scale Application Quickly

### Scenario

Traffic suddenly increases.

### Solution

Scale deployment.

```bash
kubectl scale deployment myapp --replicas=10
```

Or use **Horizontal Pod Autoscaler**

```bash
kubectl autoscale deployment myapp --cpu-percent=50 --min=2 --max=10
```

---

# 15. Container Inside Pod Needs Debugging

### Scenario

Application not working and you need to debug inside container.

### Solution

Execute shell inside pod

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

Or check logs

```bash
kubectl logs <pod-name>
```

---

# ⭐ Most Important Kubernetes Debug Commands

| Command                | Purpose                       |
| ---------------------- | ----------------------------- |
| `kubectl get pods`     | Check pod status              |
| `kubectl describe pod` | View detailed info            |
| `kubectl logs`         | Application logs              |
| `kubectl exec`         | Run commands inside container |
| `kubectl get events`   | View cluster events           |
| `kubectl top pod`      | Resource usage                |

---

💡 **Real DevOps Interview Tip**

Most interviewers test **3 Kubernetes troubleshooting areas**:

1️⃣ **Pod Issues**

* CrashLoopBackOff
* Pending

2️⃣ **Networking Issues**

* Service not reachable
* DNS problems

3️⃣ **Storage Issues**

* PV/PVC mounting
* Data persistence

---
Here are **25 Advanced Kubernetes Interview Questions** commonly asked in **DevOps / SRE / Cloud Engineer interviews**. These test **architecture understanding, internal components, scaling, networking, and production troubleshooting**. 🚀

---

# 25 Advanced Kubernetes Interview Questions (with Answers)

---

# 1. What happens internally when you run `kubectl apply`?

**Answer**

Steps inside Kubernetes:

1. `kubectl` sends request to **API Server**
2. API Server validates request
3. Object stored in **etcd**
4. Scheduler assigns node
5. Kubelet on node creates pod
6. Container runtime starts container

---

# 2. What is etcd in Kubernetes?

**Answer**

`etcd` is a **distributed key-value store** used by Kubernetes to store cluster state.

Stores:

* Pod configuration
* Secrets
* ConfigMaps
* Cluster state
* Node information

It is the **single source of truth** for Kubernetes.

---

# 3. What is the difference between Deployment and StatefulSet?

| Deployment           | StatefulSet        |
| -------------------- | ------------------ |
| Stateless apps       | Stateful apps      |
| Pods interchangeable | Pods have identity |
| Random pod names     | Ordered pod names  |
| Example: web apps    | Example: databases |

Example StatefulSet pods:

```
mysql-0
mysql-1
mysql-2
```

---

# 4. What is the difference between DaemonSet and Deployment?

| Deployment                   | DaemonSet              |
| ---------------------------- | ---------------------- |
| Runs specific number of pods | Runs one pod per node  |
| Used for apps                | Used for node services |

Examples of DaemonSet:

* Logging agents
* Monitoring agents
* Network plugins

Examples:

* Fluentd
* Prometheus Node Exporter

---

# 5. What are Kubernetes namespaces?

**Answer**

Namespaces logically divide a Kubernetes cluster.

Example:

```
dev
staging
production
```

Check namespaces:

```bash
kubectl get namespaces
```

---

# 6. What is the Kubernetes control plane?

Control plane manages cluster.

Components:

* API Server
* Scheduler
* Controller Manager
* etcd
* Cloud Controller Manager

---

# 7. What is kubelet?

**Answer**

`kubelet` runs on each worker node.

Responsibilities:

* Communicates with API Server
* Starts containers
* Monitors pods
* Reports node status

---

# 8. What is kube-proxy?

**Answer**

`kube-proxy` manages **networking rules**.

Responsibilities:

* Service routing
* Load balancing
* Network forwarding

Uses:

* iptables
* IPVS

---

# 9. What is a Kubernetes Service?

Service exposes pods using a **stable IP address**.

Types:

| Service Type | Purpose                |
| ------------ | ---------------------- |
| ClusterIP    | Internal access        |
| NodePort     | Expose on node port    |
| LoadBalancer | External load balancer |
| ExternalName | External service       |

---

# 10. What is Ingress?

Ingress manages **external HTTP/HTTPS access** to services.

Example features:

* Load balancing
* SSL termination
* Path routing
* Domain routing

Example:

```
example.com/api
example.com/web
```

---

# 11. What is Horizontal Pod Autoscaler (HPA)?

Automatically scales pods based on metrics.

Example:

```
CPU usage
Memory usage
Custom metrics
```

Example command:

```bash
kubectl autoscale deployment app --cpu-percent=50 --min=2 --max=10
```

---

# 12. What is Vertical Pod Autoscaler?

Adjusts **CPU and memory of pods automatically**.

Example:

```
Increase memory if usage high
```

Unlike HPA which adds pods.

---

# 13. What are Taints and Tolerations?

They control **which pods can run on which nodes**.

Example taint:

```
node-role=database:NoSchedule
```

Pod must have **toleration** to run there.

---

# 14. What is Node Affinity?

Controls **pod scheduling based on node labels**.

Example:

```
run pods only on SSD nodes
```

Example:

```yaml
nodeSelector:
  disktype: ssd
```

---

# 15. What is Pod Affinity and Anti-Affinity?

Pod affinity → schedule pods **together**.

Example:

```
Frontend near backend
```

Pod anti-affinity → schedule pods **separately**.

Example:

```
Spread replicas across nodes
```

---

# 16. What is a ConfigMap?

Stores **configuration data** separate from application.

Example:

```
database_url
api_endpoint
```

Create ConfigMap:

```bash
kubectl create configmap app-config --from-file=config.txt
```

---

# 17. What are Kubernetes Secrets?

Secrets store **sensitive data**.

Examples:

* passwords
* API keys
* tokens
* certificates

Example:

```bash
kubectl create secret generic db-secret --from-literal=password=123
```

---

# 18. What is a Persistent Volume (PV)?

A **cluster storage resource**.

Example storage:

* NFS
* AWS EBS
* Azure Disk
* Google Persistent Disk

---

# 19. What is Persistent Volume Claim (PVC)?

PVC is a **request for storage**.

Example:

```
App requests 10GB storage
```

Kubernetes binds PVC to PV.

---

# 20. What is Kubernetes CNI?

CNI = **Container Network Interface**

Provides pod networking.

Popular CNI plugins:

* Calico
* Flannel
* Weave
* Cilium

---

# 21. What is Rolling Update?

Deployment strategy to update pods **without downtime**.

Steps:

1. Create new pod
2. Remove old pod
3. Repeat gradually

Example:

```
v1 → v2 update
```

---

# 22. What is Canary Deployment?

Gradually deploy new version to small subset.

Example:

```
90% → old version
10% → new version
```

If stable → increase traffic.

---

# 23. What is Blue-Green Deployment?

Two environments:

```
Blue → old version
Green → new version
```

Traffic switches instantly.

Benefits:

* Zero downtime
* Easy rollback

---

# 24. How does Kubernetes handle container failures?

Using **self-healing mechanisms**:

* Restart containers
* Replace failed pods
* Reschedule pods on other nodes

Controllers handle this automatically.

---

# 25. How do you debug a Kubernetes cluster?

Common troubleshooting commands:

Check pods

```bash
kubectl get pods
```

Check logs

```bash
kubectl logs pod-name
```

Describe resource

```bash
kubectl describe pod pod-name
```

Check events

```bash
kubectl get events
```

Access pod shell

```bash
kubectl exec -it pod-name -- /bin/bash
```

---

# ⭐ Real DevOps Interview Tip

Advanced interviews usually focus on **these Kubernetes areas**:

### 1️⃣ Scheduling

* Node affinity
* Taints & tolerations
* Pod affinity

### 2️⃣ Networking

* Services
* Ingress
* CNI

### 3️⃣ Storage

* PV
* PVC
* StatefulSets

### 4️⃣ Scaling

* HPA
* VPA

### 5️⃣ Deployments

* Rolling updates
* Blue-green
* Canary

---





Below are **20 Kubernetes Production Troubleshooting Scenarios** that DevOps engineers commonly face in **real production environments**. These questions are frequently asked in **DevOps/SRE interviews** because they test **debugging skills and Kubernetes internals**. 🚀

---

# 20 Kubernetes Production Troubleshooting Scenarios

---

# 1. Pod is in CrashLoopBackOff

### Scenario

A pod keeps restarting repeatedly.

### Troubleshooting

Check logs

```bash
kubectl logs <pod-name>
```

Check events

```bash
kubectl describe pod <pod-name>
```

### Possible Causes

* Application crash
* Missing environment variables
* ConfigMap/Secret issues
* Database connection failure

---

# 2. Pod Stuck in Pending State

### Scenario

Pod is not scheduled on any node.

### Troubleshooting

```bash
kubectl describe pod <pod-name>
```

### Common Reasons

* Insufficient CPU or memory
* Node selector mismatch
* Taints without tolerations
* PVC not available

---

# 3. Pod Running but Service Not Accessible

### Scenario

Pod is running but application cannot be accessed.

### Check

```bash
kubectl get svc
kubectl describe svc <service-name>
```

Verify:

* Service selectors match pod labels
* Correct targetPort

---

# 4. Node Status Shows NotReady

### Scenario

One of the worker nodes becomes unavailable.

### Troubleshooting

```bash
kubectl get nodes
kubectl describe node <node-name>
```

Check on node

```
systemctl status kubelet
```

Possible issues:

* kubelet stopped
* network issue
* disk pressure

---

# 5. ImagePullBackOff Error

### Scenario

Pod cannot pull container image.

### Troubleshooting

```bash
kubectl describe pod <pod-name>
```

Possible causes:

* Wrong image name
* Private registry authentication
* Network issue

---

# 6. ConfigMap Updated but Application Not Reflecting Changes

### Reason

Pods do not automatically reload ConfigMaps.

### Fix

Restart deployment

```bash
kubectl rollout restart deployment <deployment-name>
```

---

# 7. Pod Cannot Connect to Another Pod

### Scenario

Backend cannot connect to database.

### Troubleshooting

Check service

```bash
kubectl get svc
```

Test DNS inside pod

```bash
kubectl exec -it <pod> -- nslookup mysql
```

---

# 8. High CPU Usage in Cluster

### Scenario

Cluster performance is slow.

### Troubleshooting

Check resource usage

```bash
kubectl top nodes
kubectl top pods
```

Solution:

* Set resource limits
* Scale pods
* Use HPA

---

# 9. Deployment Update Fails

### Scenario

New deployment version fails.

### Troubleshooting

Check rollout status

```bash
kubectl rollout status deployment <deployment>
```

Rollback

```bash
kubectl rollout undo deployment <deployment>
```

---

# 10. Persistent Volume Not Mounting

### Scenario

Pod cannot start because volume not mounted.

### Troubleshooting

```bash
kubectl get pv
kubectl get pvc
kubectl describe pod <pod>
```

Common issues:

* Storage class mismatch
* PV not bound

---

# 11. DNS Resolution Not Working

### Scenario

Pods cannot resolve service names.

### Troubleshooting

Check DNS

```bash
kubectl exec -it <pod> -- nslookup kubernetes.default
```

Check CoreDNS

```bash
kubectl get pods -n kube-system
```

---

# 12. Pods Restarting Frequently

### Scenario

Pods restart randomly.

### Check

```bash
kubectl describe pod <pod>
```

Possible reasons

* Liveness probe failure
* OOMKilled
* Application crash

---

# 13. Ingress Not Routing Traffic

### Scenario

External traffic not reaching services.

### Troubleshooting

Check ingress

```bash
kubectl get ingress
```

Verify ingress controller

```bash
kubectl get pods -n ingress-nginx
```

---

# 14. Disk Pressure on Node

### Scenario

Pods not scheduled because node disk is full.

### Troubleshooting

```bash
kubectl describe node <node>
```

Solution

* Clean logs
* Remove unused images
* Increase storage

---

# 15. Pod OOMKilled

### Scenario

Container killed due to memory limits.

### Check

```bash
kubectl describe pod <pod>
```

Increase memory limits

Example:

```yaml
resources:
  limits:
    memory: "1Gi"
```

---

# 16. Pods Scheduled on Wrong Node

### Scenario

Sensitive workloads run on incorrect nodes.

### Solution

Use **node affinity**

Example:

```yaml
nodeSelector:
  disktype: ssd
```

---

# 17. Application Downtime During Deployment

### Scenario

Deployment update causes downtime.

### Solution

Use rolling updates.

Example

```yaml
strategy:
  type: RollingUpdate
```

---

# 18. Secrets Not Accessible to Pod

### Scenario

Application cannot read secret values.

### Troubleshooting

Check secrets

```bash
kubectl get secrets
```

Check pod configuration

```bash
kubectl describe pod <pod>
```

---

# 19. Pods Not Distributed Across Nodes

### Scenario

All pods scheduled on one node.

### Solution

Use **pod anti-affinity**.

Example

```yaml
podAntiAffinity:
```

This spreads pods across nodes.

---

# 20. API Server Slow or Unresponsive

### Scenario

Cluster commands take long time.

### Possible Causes

* etcd latency
* high API traffic
* resource exhaustion

### Troubleshooting

Check control plane pods

```bash
kubectl get pods -n kube-system
```

Check etcd health.

---

# ⭐ Kubernetes Production Debugging Commands (Very Important)

| Command                | Purpose           |
| ---------------------- | ----------------- |
| `kubectl get pods -A`  | Check all pods    |
| `kubectl describe pod` | Detailed pod info |
| `kubectl logs`         | Application logs  |
| `kubectl exec`         | Debug inside pod  |
| `kubectl get events`   | Cluster events    |
| `kubectl top pods`     | Resource usage    |

---

# 💡 Real DevOps Interview Tip

Production troubleshooting usually focuses on **5 main areas**:

### 1️⃣ Pod Issues

* CrashLoopBackOff
* Pending

### 2️⃣ Networking

* Service not reachable
* DNS issues

### 3️⃣ Storage

* PV/PVC problems

### 4️⃣ Resources

* OOMKilled
* CPU spikes

### 5️⃣ Deployments

* Failed rollouts
* Downtime

---








Kubernetes interviews often test whether you can **read, write, and debug YAML files**. Below are **15 Kubernetes YAML-based interview questions** with explanations and examples. These are commonly asked for **DevOps fresher / junior roles**. 🚀

---

# 1. Write a YAML to create a simple Pod

### Question

Create a Pod running an nginx container.

### Answer

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

Key fields:

* `apiVersion` → Kubernetes API version
* `kind` → Resource type
* `metadata` → Name and labels
* `spec` → Desired configuration

---

# 2. Write a Deployment YAML with 3 replicas

### Answer

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
```

Important fields:

* `replicas`
* `selector`
* `template`

---

# 3. Write YAML to expose a Deployment using a Service

### Answer

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007
```

Service types:

* ClusterIP
* NodePort
* LoadBalancer

---

# 4. How do you define environment variables in YAML?

### Answer

```yaml
containers:
- name: app
  image: myapp
  env:
  - name: DATABASE_HOST
    value: mysql
```

You can also use **ConfigMaps or Secrets**.

---

# 5. How do you use a ConfigMap in YAML?

### ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: production
```

Use in Pod:

```yaml
envFrom:
- configMapRef:
    name: app-config
```

---

# 6. How do you mount a ConfigMap as a volume?

### Answer

```yaml
volumes:
- name: config-volume
  configMap:
    name: app-config
```

Mount inside container:

```yaml
volumeMounts:
- name: config-volume
  mountPath: /etc/config
```

---

# 7. Write YAML to define resource limits

### Answer

```yaml
resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "500m"
```

Purpose:

* Prevent resource starvation
* Improve scheduling

---

# 8. Write YAML for Persistent Volume Claim

### Answer

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

---

# 9. How do you use a Secret in YAML?

### Secret definition

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: MTIzNA==
```

Use in container

```yaml
env:
- name: DB_PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-secret
      key: password
```

---

# 10. Write YAML for Node Selector

### Answer

```yaml
spec:
  nodeSelector:
    disktype: ssd
```

This schedules pod only on nodes with label:

```
disktype=ssd
```

---

# 11. How do you define liveness probe?

### Answer

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 5
```

Purpose:

Restart container if unhealthy.

---

# 12. How do you define readiness probe?

### Answer

```yaml
readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

Purpose:

Pod receives traffic **only when ready**.

---

# 13. Write YAML for Horizontal Pod Autoscaler

### Answer

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 2
  maxReplicas: 10
```

---

# 14. Write YAML for Ingress

### Answer

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
spec:
  rules:
  - host: myapp.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: app-service
            port:
              number: 80
```

---

# 15. Write YAML for a DaemonSet

### Answer

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-monitor
spec:
  selector:
    matchLabels:
      app: monitor
  template:
    metadata:
      labels:
        app: monitor
    spec:
      containers:
      - name: monitor
        image: prom/node-exporter
```

DaemonSet runs **one pod per node**.

---

# ⭐ YAML Mistakes Interviewers Check

These **5 mistakes are very common** in interviews:

### 1️⃣ Wrong indentation

YAML is indentation sensitive.

### 2️⃣ Selector mismatch

```
Deployment label ≠ Service selector
```

### 3️⃣ Missing container name

Required field.

### 4️⃣ Wrong API version

Example:

```
apps/v1 for Deployment
```

### 5️⃣ Missing selector in Deployment

---

# 💡 DevOps Interview Tip

Interviewers often give **broken YAML and ask you to fix it**.

Example problems:

* Wrong labels
* Wrong indentation
* Missing ports
* Missing selectors

---



### Summary of Kubernetes (K8s) Tutorial and Practical Guide

This comprehensive video tutorial covers Kubernetes (K8s) fundamentals, architecture, practical installation, deployment, scaling, updating applications, and persistent storage management. It is beginner-friendly and uses simple language with examples, focusing on real-world use cases, especially container orchestration with K8s.

---

### Key Topics Covered

- **Kubernetes Overview**  
  - Kubernetes is an open-source platform for automating deployment, scaling, and management of containerized applications.  
  - It solves problems like scaling, load balancing, high availability, and zero downtime deployment.  
  - Works with different infrastructure including virtual machines and cloud environments.

- **Architecture and Components**  
  - **Master (Control Plane):** Manages the cluster, schedules workloads, maintains cluster state via API Server, Scheduler, Controller Manager.  
  - **Worker Nodes:** Run containerized applications inside Pods; each node runs a Kubelet agent and Kube Proxy for networking.  
  - **Pods:** Smallest deployable unit; can contain one or multiple containers sharing resources and network.  
  - Communication among components is maintained via API Server and Kube Proxy.

- **Installation and Setup**  
  - Installation on Windows using Chocolatey and MiniKube for local Kubernetes clusters.  
  - On macOS using Homebrew and MiniKube, supporting multiple virtualization drivers (Docker, VirtualBox, Parallels).  
  - Commands for verifying installation, starting/stopping clusters, and accessing MiniKube dashboard.

- **Deploying Applications on Kubernetes**  
  - Creating deployments using `kubectl create deployment` with container images pulled from Docker Hub.  
  - Managing pods created by deployments, checking status, logs, and scaling applications with `kubectl scale`.  
  - Exposing deployments externally using Kubernetes **Service** objects (LoadBalancer type) to enable access outside the cluster.  
  - Updating running applications with zero downtime via rolling updates (`kubectl set image`) and rollback on failure.

- **Scaling and High Availability**  
  - Running multiple pod replicas to handle load and avoid single points of failure.  
  - Kubernetes automatically restarts failed pods (self-healing).  
  - Deployment of multiple instances ensures availability during pod restarts or failures.

- **Configuration Files and YAML Syntax**  
  - Managing deployments and services via YAML configuration files.  
  - Using declarative approach with `kubectl apply -f` to create/update Kubernetes resources.  
  - Configuration includes metadata, spec (replicas, containers, image names), labels, selectors, and ports.

- **Multi-Container Pods and Inter-Container Communication**  
  - Running multiple containers in a single pod to share resources and communicate via localhost.  
  - Alternatively, running containers in separate pods with communication via services.  
  - Example project with a Node.js web UI container and MongoDB container demonstrating both approaches.

- **Environment Variables and ConfigMaps**  
  - Using environment variables in pod specs for dynamic configuration, such as database host and port.  
  - Managing configuration data via Kubernetes ConfigMaps referenced in pod specs.

- **Persistent Storage and Volume Management**  
  - Problem: Container restarts cause loss of local data; solution: Persistent Volumes (PV) and Persistent Volume Claims (PVC).  
  - PV is a storage resource provisioned in the cluster (hostPath for local setups, cloud storage for production).  
  - PVC requests storage from PV for pods to use, ensuring data persists beyond pod lifecycle.  
  - Example with MongoDB deployment using PV and PVC to store data outside the pod, maintaining data after restarts.  
  - Demonstrated how data remains intact even after deleting and recreating pods/clusters.

- **Testing Persistent Storage**  
  - Stopping and restarting MiniKube cluster shows data persistence via PVC.  
  - Demonstrated storing and retrieving emails in a Node.js app connected to MongoDB using mounted volumes.

---

### Timeline Table (High-Level)

| Time Range        | Topic/Activity                                           |
|-------------------|---------------------------------------------------------|
| 00:00:00 - 00:06:50  | Introduction, Kubernetes overview, orchestration analogy, problem statement |
| 00:07:00 - 00:14:50  | Kubernetes architecture: Master, Worker nodes, components (API Server, Kubelet, Proxy, Scheduler) |
| 00:15:00 - 00:23:00  | Installation on Windows and macOS using MiniKube and kubectl |
| 00:23:00 - 00:43:00  | Basic deployments, pod creation, exposing services, accessing apps, rolling updates and rollbacks |
| 00:43:00 - 01:10:00  | React app creation, Dockerfile creation, image build/push, deployment and updates on K8s |
| 01:10:00 - 01:25:00  | Self-healing, scaling deployments, zero downtime updates, using configuration files |
| 01:25:00 - 01:50:00  | Multi-container pods, inter-container communication, example project with Node.js + MongoDB |
| 01:50:00 - 02:25:00  | Docker run commands, local app testing, multi-pod deployment, environment variables |
| 02:25:00 - 02:50:00  | Persistent Volume (PV) and Persistent Volume Claim (PVC) concepts, hostPath usage, storage classes |
| 02:50:00 - 03:03:30  | Practical PV and PVC creation, volume mounts in deployments, testing data persistence on cluster restarts |

---

### Kubernetes Core Concepts and Definitions (Markdown Table)

| Term                     | Definition/Description                                                                                              |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| **Pod**                  | Smallest deployable unit in Kubernetes; can contain one or more containers sharing network and storage.             |
| **Node**                 | Worker machine (physical or virtual) running pods.                                                                  |
| **Master (Control Plane)**| Manages cluster state, scheduling, and orchestration via API Server, Scheduler, Controller Manager.                 |
| **Deployment**            | Declarative resource to manage stateless applications; manages replica sets and pods lifecycle.                    |
| **Service**               | An abstraction to expose pods internally or externally; supports load balancing and stable network identity.         |
| **Persistent Volume (PV)**| Cluster-level storage resource provisioned to provide durable storage for pods.                                     |
| **Persistent Volume Claim (PVC)** | Request for storage by a pod, bound to a PV for persistent data usage.                                         |
| **ConfigMap**             | Kubernetes resource to manage configuration data and pass it as environment variables or config files to pods.      |
| **Kubelet**               | Agent running on each node to manage pods and containers.                                                           |
| **Kube Proxy**            | Network proxy managing communication rules inside cluster.                                                          |
| **Rolling Update**        | Updating pods with zero downtime by gradually replacing old pods with new ones.                                      |
| **Rollback**              | Reverting to previous deployment version in case of errors.                                                         |

---

### Important Commands Examples (Bulleted List)

- Install and verify Kubernetes tools:  
  `kubectl version`, `minikube start`, `minikube dashboard`  
- Create deployment:  
  `kubectl create deployment <name> --image=<image>`  
- Expose deployment:  
  `kubectl expose deployment <name> --type=LoadBalancer --port=<port>`  
- Scale deployment:  
  `kubectl scale deployment <name> --replicas=<number>`  
- Update deployment image:  
  `kubectl set image deployment/<name> <container>=<new-image>:<tag>`  
- Rollback deployment:  
  `kubectl rollout undo deployment/<name>`  
- Get status and logs:  
  `kubectl get pods`, `kubectl logs <pod-name>`  
- Apply configuration file:  
  `kubectl apply -f <filename>.yaml`  
- Create Persistent Volume and Claim:  
  `kubectl apply -f persistent-volume.yaml`  
  `kubectl apply -f persistent-volume-claim.yaml`  
- Delete resources:  
  `kubectl delete deployment <name>`, `kubectl delete service <name>`

---

### Key Insights

- **Kubernetes automates container orchestration**, ensuring application scalability, high availability, and zero downtime.  
- **Pods are the smallest unit**, can run multiple containers sharing resources and network.  
- **Master node components manage cluster state and scheduling**, while worker nodes run the actual applications.  
- **MiniKube enables local Kubernetes cluster setup** for learning and testing.  
- **Deployments manage replica sets and pod lifecycle**, supporting rolling updates and rollbacks efficiently.  
- **Services expose applications externally and internally**, enabling stable access and load balancing.  
- **Persistent Volumes and Claims ensure data persistence**, solving container data loss on restarts.  
- **Environment variables and ConfigMaps provide dynamic configuration support.**  
- **Multi-container pods and multi-pod applications can communicate via localhost or services respectively.**  
- **Kubernetes self-healing automatically restarts failed pods**, maintaining app availability.  
- **Scaling is simple and effective with `kubectl scale`, handling traffic spikes seamlessly.**  
- **Use of YAML files standardizes configuration, making deployments reproducible and manageable.**  
- **Persistent storage should ideally be outside pods and containers**, using PVs and PVCs to avoid data loss.  
- **Local hostPath volumes are suited for single-node setups; multi-node clusters require network or cloud storage solutions.**  
- **Troubleshooting tools like logs and dashboard provide visibility into cluster health and issues.**

---

### Conclusion

This tutorial provides a detailed understanding of Kubernetes concepts, architecture, installation, application lifecycle management, scaling, updating, and persistent storage handling. By following the examples and command demonstrations, beginners can confidently deploy containerized applications, handle real-world scenarios like rolling updates, ensure zero downtime, and manage persistent data effectively in Kubernetes clusters.

Practicing these steps and commands will help users master Kubernetes fundamentals and apply them in various environments, from local setups using MiniKube to production-grade multi-node clusters integrating cloud storage solutions.



---
---
---
---
------
---
---
---
---
---
---
---
---
---
---
---
---
------
---
---
---
---
---
---
---
---
---
---
---
---
------
---
---
---
---
---
---
---
---








To create a **Docker Compose setup** for your **SafeMind project (ReactJS + Spring Boot + MySQL)**, you basically containerize each part of the system and orchestrate them together using **docker-compose.yml**.

Your architecture will look like this:

```
SafeMind
│
├── frontend  (ReactJS)
├── backend   (Spring Boot - J2EE)
└── database  (MySQL)
```

Docker Compose will run **3 containers**:

1. React frontend
2. Spring Boot backend
3. MySQL database

---

# 1. Project Folder Structure

Create a clean structure like this:

```
safemind/
│
├── docker-compose.yml
│
├── backend/
│   ├── Dockerfile
│   ├── pom.xml
│   └── src/
│
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   └── src/
│
└── mysql/
    └── init.sql   (optional)
```

---

# 2. Dockerfile for Spring Boot Backend

Inside **backend/Dockerfile**

```dockerfile
FROM openjdk:17-jdk-slim

WORKDIR /app

COPY target/safemind.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]
```

Build your jar first:

```
mvn clean package
```

It will generate

```
target/safemind.jar
```

---

# 3. Dockerfile for React Frontend

Inside **frontend/Dockerfile**

```dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

RUN npm install -g serve

EXPOSE 3000

CMD ["serve","-s","build","-l","3000"]
```

---

# 4. MySQL Configuration

Optional **mysql/init.sql**

```sql
CREATE DATABASE safemind;
```

---

# 5. Create docker-compose.yml

In root folder:

```yaml
version: "3.8"

services:

  mysql:
    image: mysql:8
    container_name: safemind_mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: safemind
    ports:
      - "3307:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  backend:
    build: ./backend
    container_name: safemind_backend
    depends_on:
      - mysql
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/safemind
      SPRING_DATASOURCE_USERNAME: root
      SPRING_DATASOURCE_PASSWORD: root

  frontend:
    build: ./frontend
    container_name: safemind_frontend
    depends_on:
      - backend
    ports:
      - "3000:3000"

volumes:
  mysql_data:
```

Important thing:

```
mysql
```

is the **hostname** inside Docker network.

So Spring Boot connects using:

```
jdbc:mysql://mysql:3306/safemind
```

NOT `localhost`.

---

# 6. Update Spring Boot application.properties

In your backend:

```
spring.datasource.url=jdbc:mysql://mysql:3306/safemind
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
```

---

# 7. Run Everything

From root directory:

```
docker compose up --build
```

Docker will:

1. Build React container
2. Build Spring Boot container
3. Pull MySQL image
4. Start all containers together

---

# 8. Access the Application

Frontend

```
http://localhost:3000
```

Backend API

```
http://localhost:8080
```

MySQL

```
localhost:3307
```

---

# 9. Check Containers

```
docker ps
```

You should see:

```
safemind_frontend
safemind_backend
safemind_mysql
```

---

# 10. Stop Containers

```
docker compose down
```

---

# 11. Extra (Best Practice for Resume / GitHub)

Add this to README:

```
# Run with Docker

docker compose up --build
```

This makes your project **much more professional for recruiters**.

---

💡 **Pro Tip (Important for your project):**

Since you used **WebRTC video consultation**, Docker Compose may need additional ports if you use:

* **STUN/TURN server**
* **WebSocket signaling**

Example:

```
3478 (TURN)
8081 (WebSocket)
```

---




---
---
---
---
------
---
---
---
---
---
---
---
---








I’ll explain your **`docker-compose.yml` line-by-line** so you understand **what each line does and why it is needed**. This understanding is important because in interviews they often ask *“Explain your Docker Compose architecture.”*

Here is the compose file again for reference:

```yaml
version: "3.8"

services:

  mysql:
    image: mysql:8
    container_name: safemind_mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: safemind
    ports:
      - "3307:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  backend:
    build: ./backend
    container_name: safemind_backend
    depends_on:
      - mysql
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/safemind
      SPRING_DATASOURCE_USERNAME: root
      SPRING_DATASOURCE_PASSWORD: root

  frontend:
    build: ./frontend
    container_name: safemind_frontend
    depends_on:
      - backend
    ports:
      - "3000:3000"

volumes:
  mysql_data:
```

---

# 1️⃣ `version: "3.8"`

### What it is

Defines the **Docker Compose file format version**.

### Why it is written

Different Docker Compose versions support different features.

`3.8` is commonly used because it supports:

* networks
* volumes
* container dependencies
* modern Docker features

Without this line Docker may not know how to interpret the file.

---

# 2️⃣ `services:`

### What it is

This is the **main section where you define containers**.

### Why it is written

Your application has **multiple components**, and each component runs in its own container.

In your case:

* MySQL database
* Spring Boot backend
* React frontend

Each one becomes a **service**.

---

# 3️⃣ `mysql:` (Service name)

```yaml
mysql:
```

### What it is

Defines the **database container**.

### Why it is written

Your Spring Boot application needs **MySQL** to store:

* user accounts
* therapist profiles
* appointments
* journals
* mood tracking

Instead of installing MySQL manually, Docker runs it in a container.

The name **`mysql`** also becomes the **hostname inside the Docker network**.

So backend connects using:

```
jdbc:mysql://mysql:3306/safemind
```

---

# 4️⃣ `image: mysql:8`

```yaml
image: mysql:8
```

### What it is

Tells Docker to use the **official MySQL version 8 image** from Docker Hub.

### Why it is written

Instead of building MySQL yourself, Docker pulls a ready-made image.

Benefits:

* quick setup
* reliable
* production tested

---

# 5️⃣ `container_name: safemind_mysql`

```yaml
container_name: safemind_mysql
```

### What it is

Gives the container a **custom name**.

### Why it is written

If not provided, Docker generates random names like:

```
amazing_turing
happy_fermi
```

With this:

```
safemind_mysql
```

You can easily manage containers.

Example:

```bash
docker logs safemind_mysql
docker stop safemind_mysql
```

---

# 6️⃣ `restart: always`

```yaml
restart: always
```

### What it is

Defines the **restart policy**.

### Why it is written

If the container crashes or Docker restarts, MySQL will **automatically restart**.

Useful for:

* production
* avoiding manual restarts

Without this your DB might stop if something fails.

---

# 7️⃣ `environment:`

```yaml
environment:
  MYSQL_ROOT_PASSWORD: root
  MYSQL_DATABASE: safemind
```

### What it is

Sets **environment variables inside the container**.

### Why it is written

The MySQL Docker image needs configuration values.

#### `MYSQL_ROOT_PASSWORD`

Sets password for MySQL root user.

```
username = root
password = root
```

#### `MYSQL_DATABASE`

Automatically creates the database:

```
safemind
```

Without this you'd have to manually run:

```
CREATE DATABASE safemind;
```

---

# 8️⃣ `ports:`

```yaml
ports:
  - "3307:3306"
```

### What it is

Maps **host machine port → container port**.

Format:

```
HOST_PORT:CONTAINER_PORT
```

### Why it is written

MySQL inside container runs on:

```
3306
```

But your local machine may already have MySQL.

So we expose it as:

```
localhost:3307
```

Meaning:

```
Your PC port → Container port
3307 → 3306
```

Now you can connect using:

```
localhost:3307
```

---

# 9️⃣ `volumes:`

```yaml
volumes:
  - mysql_data:/var/lib/mysql
```

### What it is

Creates **persistent storage**.

### Why it is written

Normally containers are **temporary**.

If container stops, data would be lost.

But MySQL stores data in:

```
/var/lib/mysql
```

So we mount a Docker volume:

```
mysql_data
```

This ensures:

* DB data persists
* container can be deleted safely

---

# 🔟 Backend Service

```yaml
backend:
```

Defines your **Spring Boot application container**.

This runs your:

* authentication
* appointment APIs
* mood tracking
* journal encryption
* WebRTC signaling

---

# 1️⃣1️⃣ `build: ./backend`

```yaml
build: ./backend
```

### What it is

Tells Docker to **build an image using the Dockerfile in `/backend` folder**.

### Why it is written

Because your backend is **custom code**.

Docker will:

1️⃣ read `backend/Dockerfile`
2️⃣ build the image
3️⃣ run container

---

# 1️⃣2️⃣ `container_name`

```yaml
container_name: safemind_backend
```

Same idea as MySQL.

Makes container easy to manage.

---

# 1️⃣3️⃣ `depends_on`

```yaml
depends_on:
  - mysql
```

### What it is

Ensures **MySQL starts before backend**.

### Why it is written

Spring Boot requires database connection at startup.

If backend starts first:

```
DB connection failed
```

So Compose starts:

```
1️⃣ MySQL
2️⃣ Backend
```

---

# 1️⃣4️⃣ `ports`

```yaml
ports:
  - "8080:8080"
```

### What it is

Maps backend port to host.

Spring Boot runs on:

```
8080
```

Now you can access API at:

```
http://localhost:8080
```

---

# 1️⃣5️⃣ Backend Environment Variables

```yaml
environment:
  SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/safemind
  SPRING_DATASOURCE_USERNAME: root
  SPRING_DATASOURCE_PASSWORD: root
```

### What it is

Configures Spring Boot database connection.

### Why it is written

Inside Docker, **containers communicate using service names**.

So:

```
mysql
```

is the hostname.

NOT:

```
localhost
```

Because `localhost` inside container refers to the container itself.

So correct connection is:

```
jdbc:mysql://mysql:3306/safemind
```

---

# 1️⃣6️⃣ Frontend Service

```yaml
frontend:
```

Defines your **ReactJS UI container**.

This includes:

* login UI
* therapist dashboard
* appointment booking
* mood tracking
* WebRTC video interface

---

# 1️⃣7️⃣ `build: ./frontend`

Docker builds image using:

```
frontend/Dockerfile
```

Which:

1️⃣ installs Node
2️⃣ builds React
3️⃣ serves static files

---

# 1️⃣8️⃣ `depends_on`

```yaml
depends_on:
  - backend
```

Ensures backend starts before frontend.

Because frontend will call APIs like:

```
http://backend:8080/api
```

---

# 1️⃣9️⃣ Frontend Ports

```yaml
ports:
  - "3000:3000"
```

React app becomes available at:

```
http://localhost:3000
```

---

# 2️⃣0️⃣ Volumes Section

```yaml
volumes:
  mysql_data:
```

### What it is

Defines a **named Docker volume**.

### Why it is written

Used earlier here:

```
mysql_data:/var/lib/mysql
```

This creates persistent storage managed by Docker.

Without declaring it here, Compose may fail.

---

# 🔑 Final Architecture

Your compose file creates this system:

```
           +----------------+
           |   React App    |
           |   (Frontend)   |
           |   Port 3000    |
           +--------+-------+
                    |
                    v
           +----------------+
           |  Spring Boot   |
           |    Backend     |
           |    Port 8080   |
           +--------+-------+
                    |
                    v
           +----------------+
           |     MySQL      |
           |   Database     |
           |    Port 3306   |
           +----------------+
```

All containers communicate inside a **Docker network** automatically created by Docker Compose.

---

# 🔥 Interview Tip

If interviewer asks **“Why Docker Compose?”**

You can say:

> Docker Compose allows us to run a multi-container architecture (React frontend, Spring Boot backend, and MySQL database) using a single configuration file. It ensures service dependency management, consistent environments, and simplified deployment using one command.

```
docker compose up --build
```

---

If you want, I can also show you **3 advanced improvements** that will make your Docker setup **look like a production system used in startups (Nginx + multi-stage builds + .env secrets)**. 🚀

















