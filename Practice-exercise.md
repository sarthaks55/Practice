# Docker Exercise
# 🧪 Exercise 1 — Run Your First Container

### 🎯 Goal

Run a simple container and understand lifecycle basics.

### 🪜 Try This

1. Pull an image (`nginx`)
2. Run a container
3. Check running containers
4. Stop it
5. Remove it

---

### ✅ Solution

```bash
# Pull image
docker pull nginx

# Run container
docker run -d --name my-nginx -p 8080:80 nginx

# Check running containers
docker ps

# Stop container
docker stop my-nginx

# Remove container
docker rm my-nginx
```

👉 Open browser: `http://localhost:8080`

---

# 🧪 Exercise 2 — Interactive Container (Linux Practice)

### 🎯 Goal

Use Docker like a mini Linux machine.

### 🪜 Try This

1. Run Ubuntu container interactively
2. Install `curl`
3. Try hitting a website
4. Exit container

---

### ✅ Solution

```bash
docker run -it ubuntu bash

# inside container
apt update
apt install -y curl
curl https://example.com

# exit
exit
```

---

# 🧪 Exercise 3 — Create Your Own Docker Image

### 🎯 Goal

Understand Dockerfile basics.

### 🪜 Try This

1. Create a simple Node.js app
2. Write Dockerfile
3. Build image
4. Run container

---

### 🧾 Sample App (`app.js`)

```js
const http = require('http');

http.createServer((req, res) => {
  res.end("Hello from Docker!");
}).listen(3000);
```

---

### 🪜 Dockerfile (try writing yourself first)

---

### ✅ Solution

```Dockerfile
FROM node:18

WORKDIR /app

COPY app.js .

EXPOSE 3000

CMD ["node", "app.js"]
```

```bash
# Build image
docker build -t my-node-app .

# Run container
docker run -p 3000:3000 my-node-app
```

👉 Visit: `http://localhost:3000`

---

# 🧪 Exercise 4 — Volume (Persist Data)

### 🎯 Goal

Understand data persistence.

### 🪜 Try This

1. Run a container with a volume
2. Create a file inside container
3. Stop and remove container
4. Run again and check file exists

---

### ✅ Solution

```bash
docker run -it -v mydata:/data ubuntu bash

# inside container
echo "hello docker" > /data/file.txt
exit

# remove container
docker rm <container_id>

# run again
docker run -it -v mydata:/data ubuntu bash

cat /data/file.txt
```

👉 File should still exist ✔️

---

# 🧪 Exercise 5 — Multi-Container App (Docker Compose)

### 🎯 Goal

Run app + database together.

### 🪜 Try This

1. Create `docker-compose.yml`
2. Add:

   * Node app
   * MongoDB
3. Start both services

---

### ✅ Solution

```yaml
version: '3'
services:
  app:
    image: node:18
    container_name: node-app
    working_dir: /app
    volumes:
      - .:/app
    command: node app.js
    ports:
      - "3000:3000"

  mongo:
    image: mongo
    container_name: mongo-db
    ports:
      - "27017:27017"
```

```bash
docker-compose up
```

---

# 🧪 Exercise 6 — Debugging (Important Skill)

### 🎯 Goal

Learn how to debug broken containers.

### 🪜 Try This

1. Run a container that exits immediately
2. Check logs
3. Enter container

---

### ✅ Solution

```bash
docker logs <container_id>

docker exec -it <container_id> bash
```

👉 Tip: Use:

```bash
docker ps -a
```

---

# 🧪 Exercise 7 — Build a Real Project (Mini Challenge)

### 🎯 Goal

Combine everything.

### 🪜 Try This

Build:

* Backend (Node)
* Database (Mongo)
* Use Dockerfile
* Use docker-compose
* Add volume for DB

---

### ✅ Solution Structure

```
project/
 ├── app.js
 ├── Dockerfile
 ├── docker-compose.yml
```

---

### docker-compose.yml

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

---





Great—now we move from **basic usage → real-world, job-level Docker skills**.
This phase is where most people either level up… or stay stuck running `docker run`.

Below are **hands-on, slightly harder exercises** that simulate real developer tasks.

---

# 🧪 Exercise 8 — Custom Network (Container Communication)

### 🎯 Goal

Make two containers talk to each other (like backend ↔ database)

---

### 🪜 Try This

1. Create a custom network
2. Run MongoDB container
3. Run Node container
4. Connect using container name (NOT localhost)

---

### ✅ Solution

```bash
# Create network
docker network create my-network

# Run Mongo
docker run -d --name mongo --network my-network mongo

# Run Node container
docker run -it --name node-app --network my-network node:18 bash
```

Inside Node container:

```bash
apt update && apt install -y curl
```

👉 Key idea:

* Use `mongo` as hostname (NOT localhost)

---

# 🧪 Exercise 9 — Environment Variables

### 🎯 Goal

Pass config (like DB URL) into containers.

---

### 🪜 Try This

1. Run container with env variable
2. Print it inside container
3. Use it in Node app

---

### ✅ Solution

```bash
docker run -e MY_NAME=Rahul ubuntu env
```

Node example:

```js
console.log(process.env.MY_NAME);
```

👉 With compose:

```yaml
environment:
  - DB_URL=mongodb://mongo:27017
```

---

# 🧪 Exercise 10 — Bind Mount (Live Code Editing)

### 🎯 Goal

Edit code on host → reflect instantly in container.

---

### 🪜 Try This

1. Run Node container
2. Mount current folder
3. Change code → see output change

---

### ✅ Solution

```bash
docker run -it -p 3000:3000 -v $(pwd):/app -w /app node:18 node app.js
```

👉 This is how dev environments work 🔥

---

# 🧪 Exercise 11 — Multi-Stage Build (Important for Interviews)

### 🎯 Goal

Reduce image size (very important in real projects)

---

### 🪜 Try This

1. Build app in one stage
2. Run in smaller image

---

### ✅ Solution

```Dockerfile
# Build stage
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install

# Production stage
FROM node:18-slim
WORKDIR /app
COPY --from=build /app .
CMD ["node", "app.js"]
```

👉 Why?

* Smaller image
* Faster deployment
* Cleaner builds

---

# 🧪 Exercise 12 — Docker Ignore (Hidden but Powerful)

### 🎯 Goal

Avoid sending unnecessary files

---

### 🪜 Try This

Create `.dockerignore`

---

### ✅ Solution

```
node_modules
.git
.env
```

👉 Without this → builds become slow and messy

---

# 🧪 Exercise 13 — Health Check

### 🎯 Goal

Check if container is actually working

---

### 🪜 Try This

Add health check to Dockerfile

---

### ✅ Solution

```Dockerfile
HEALTHCHECK CMD curl --fail http://localhost:3000 || exit 1
```

Check:

```bash
docker ps
```

---

# 🧪 Exercise 14 — Restart Policies

### 🎯 Goal

Auto-restart crashed containers

---

### 🪜 Try This

Run container with restart policy

---

### ✅ Solution

```bash
docker run -d --restart always nginx
```

Options:

* `always`
* `on-failure`
* `unless-stopped`

---

# 🧪 Exercise 15 — Logs & Debugging (Real Skill)

### 🎯 Goal

Debug production issues

---

### 🪜 Try This

1. Run app
2. Check logs
3. Follow logs live

---

### ✅ Solution

```bash
docker logs <container_id>

docker logs -f <container_id>
```

---

# 🧪 Exercise 16 — Resource Limits

### 🎯 Goal

Control CPU & memory (important in cloud)

---

### 🪜 Try This

Limit container memory

---

### ✅ Solution

```bash
docker run -d -m 256m nginx
```

---

# 🧪 Exercise 17 — Full Production Setup (Mini Project)

### 🎯 Goal

Simulate real backend system

---

### 🪜 Build This:

* Node API
* MongoDB
* Environment variables
* Volumes
* Network
* Docker Compose

---

### ✅ Example

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_URL=mongodb://mongo:27017/test
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

---



Perfect choice—this is where Docker actually starts feeling *real*.
We’ll build something close to a production setup step by step.

---

# 🚀 PROJECT 1 — Dockerize a Full MERN-style App (Backend + DB)

We’ll keep frontend optional for now and focus on:

* Node.js API
* MongoDB
* Dockerfile
* Docker Compose
* Environment variables
* Volumes

---

## 🎯 Goal

Run a backend API connected to MongoDB using Docker (like a real backend service)

---

## 🪜 Step 1 — Create Project

```
project/
 ├── app.js
 ├── package.json
 ├── Dockerfile
 ├── docker-compose.yml
 ├── .dockerignore
```

---

## 🪜 Step 2 — Backend Code

### `app.js`

```js
const express = require('express');
const mongoose = require('mongoose');

const app = express();

const DB = process.env.DB_URL;

mongoose.connect(DB)
  .then(() => console.log("Mongo Connected"))
  .catch(err => console.log(err));

app.get('/', (req, res) => {
  res.send("API is running");
});

app.listen(3000, () => console.log("Server started"));
```

---

### `package.json`

```json
{
  "name": "docker-app",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.0"
  }
}
```

---

## 🪜 Step 3 — Dockerfile

👉 Try yourself first

---

### ✅ Solution

```Dockerfile
FROM node:18

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

---

## 🪜 Step 4 — .dockerignore

```id="l6dwhs"
node_modules
.git
.env
```

---

## 🪜 Step 5 — docker-compose.yml

👉 Try writing first

---

### ✅ Solution

```yaml
version: '3'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_URL=mongodb://mongo:27017/test
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

---

## 🪜 Step 6 — Run Project

```bash id="u7nvwp"
docker-compose up --build
```

👉 Visit:
`http://localhost:3000`

---

# 🔥 PROJECT 2 — Add Nginx Reverse Proxy

Now we simulate real production architecture:

```
Client → Nginx → Node App
```

---

## 🎯 Goal

Route traffic through Nginx (like real servers)

---

## 🪜 Step 1 — Create `nginx.conf`

```nginx
events {}

http {
  server {
    listen 80;

    location / {
      proxy_pass http://app:3000;
    }
  }
}
```

---

## 🪜 Step 2 — Update docker-compose

---

### ✅ Solution

```yaml
version: '3'

services:
  app:
    build: .
    expose:
      - "3000"
    environment:
      - DB_URL=mongodb://mongo:27017/test
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongo-data:/data/db

  nginx:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - app

volumes:
  mongo-data:
```

---

## 🪜 Step 3 — Run

```bash id="w68j3k"
docker-compose up --build
```

👉 Visit:
`http://localhost`

---

# 🔥 PROJECT 3 — Add Frontend (Optional but Powerful)

You can:

* Use React / simple HTML
* Serve via Nginx

---

## 🎯 Architecture

```
Frontend → Nginx → Backend → MongoDB
```

---

## 🪜 Simple Frontend Example

```html
<h1>Hello from Frontend</h1>
```

Serve via Nginx static folder.

---

# 🧠 Real-World Concepts You Just Learned

This is **actual production thinking**:

* Reverse proxy (Nginx)
* Service-to-service communication
* Environment-based configs
* Data persistence
* Container orchestration (Compose)

---

# ⚠️ Common Mistakes (Important)

* ❌ Using `localhost` inside containers
* ❌ Not using `.dockerignore`
* ❌ Rebuilding image for every small change
* ❌ Forgetting volumes → data loss







---
---
---
---
---
# Kubernetes 
---

# 🚀 PHASE 1 — Kubernetes Basics (Core Concepts)

Before starting, install:

* `kubectl`
* A local cluster like **Minikube** or **Kind**

👉 I’ll assume you're using **Minikube**.

```bash
minikube start
kubectl get nodes
```

---

# 🧪 Exercise 1 — Your First Pod

## 🎯 Goal

Run a container using Kubernetes (Pod)

---

## 🪜 Try This

1. Create a Pod YAML
2. Use nginx image
3. Apply it
4. Check status

---

## ✅ Solution

### `pod.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
```

```bash id="0n9v4w"
kubectl apply -f pod.yaml
kubectl get pods
```

---

# 🧪 Exercise 2 — Port Forwarding

## 🎯 Goal

Access your Pod from browser

---

## 🪜 Try This

Expose the Pod locally

---

## ✅ Solution

```bash id="lghb3o"
kubectl port-forward nginx-pod 8080:80
```

👉 Open: `http://localhost:8080`

---

# 🧪 Exercise 3 — Deployment (VERY IMPORTANT)

## 🎯 Goal

Manage pods properly (instead of raw pods)

---

## 🪜 Try This

1. Create a Deployment
2. Run 2 replicas
3. Check pods

---

## ✅ Solution

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 2
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
          ports:
            - containerPort: 80
```

```bash id="hn1y2f"
kubectl apply -f deployment.yaml
kubectl get pods
```

---

# 🧪 Exercise 4 — Service (Expose App)

## 🎯 Goal

Expose deployment via stable network

---

## 🪜 Try This

Create a Service

---

## ✅ Solution

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

```bash id="qk9p6p"
kubectl apply -f service.yaml
```

👉 Get URL:

```bash id="bn2y7m"
minikube service nginx-service
```

---

# 🧪 Exercise 5 — Scaling

## 🎯 Goal

Scale your app like real systems

---

## 🪜 Try This

Increase replicas

---

## ✅ Solution

```bash id="v8xg4a"
kubectl scale deployment nginx-deploy --replicas=5
```

Check:

```bash id="p4y3tx"
kubectl get pods
```

---

# 🧪 Exercise 6 — Rolling Updates

## 🎯 Goal

Update app without downtime

---

## 🪜 Try This

Change nginx version

---

## ✅ Solution

```bash id="rc7y5o"
kubectl set image deployment/nginx-deploy nginx=nginx:1.25
```

Check rollout:

```bash id="4p5djj"
kubectl rollout status deployment/nginx-deploy
```

Rollback:

```bash id="zj9jht"
kubectl rollout undo deployment/nginx-deploy
```

---

# 🧪 Exercise 7 — Logs & Debugging

## 🎯 Goal

Debug issues (VERY IMPORTANT)

---

## 🪜 Try This

Check logs and exec into pod

---

## ✅ Solution

```bash id="p4r7ux"
kubectl logs <pod-name>

kubectl exec -it <pod-name> -- bash
```

---

# 🧪 Exercise 8 — ConfigMap (Environment Config)

## 🎯 Goal

Separate config from code

---

## 🪜 Try This

Create ConfigMap and use it

---

## ✅ Solution

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_NAME: "MyApp"
```

Use in Deployment:

```yaml
env:
  - name: APP_NAME
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: APP_NAME
```

---

# 🧪 Exercise 9 — Persistent Volume (Storage)

## 🎯 Goal

Store data like database

---

## 🪜 Try This

Create volume and mount it

---

## ✅ Solution (simple version)

```yaml
volumeMounts:
  - mountPath: /data
    name: my-volume

volumes:
  - name: my-volume
    emptyDir: {}
```

👉 For real-world → use PersistentVolume + PVC

---

# 🧪 Exercise 10 — Full Mini Project (Important)

## 🎯 Goal

Run Node + Mongo in Kubernetes

---

## 🪜 Try This

Convert your Docker Compose app → Kubernetes

---

## ✅ Solution Overview

You will create:

1. Mongo Deployment
2. Mongo Service
3. Node Deployment
4. Node Service

---

### Mongo Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      labels:
        app: mongo
    spec:
      containers:
        - name: mongo
          image: mongo
```

---

### Mongo Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongo
spec:
  selector:
    app: mongo
  ports:
    - port: 27017
```

---

### Node Deployment (Important part)

```yaml
env:
  - name: DB_URL
    value: mongodb://mongo:27017/test
```

👉 Notice:

* Using `mongo` (service name) as hostname ✔️

---






---

# 🚀 PHASE 2 — Production-Level Kubernetes

We’ll cover:

* Ingress (proper routing like Nginx)
* Secrets (secure data)
* Autoscaling
* Real architecture thinking

---

# 🧪 Exercise 11 — Ingress (VERY IMPORTANT)

## 🎯 Goal

Expose your app like a real website (domain-based routing)

👉 Instead of:

* ❌ NodePort
* ❌ Port-forward

We use:

* ✅ Ingress (like reverse proxy)

---

## 🪜 Step 1 — Enable Ingress in Minikube

```bash
minikube addons enable ingress
```

---

## 🪜 Step 2 — Create Ingress Resource

---

### ✅ Solution

```yaml id="w9z6vq"
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
    - host: myapp.local
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

---

## 🪜 Step 3 — Map Domain Locally

Edit `/etc/hosts`:

```id="e38ws7"
<minikube-ip> myapp.local
```

Get IP:

```bash id="q0dygx"
minikube ip
```

---

👉 Open in browser:

```
http://myapp.local
```

🔥 Now this looks like a real production app.

---

# 🧪 Exercise 12 — Kubernetes Secrets

## 🎯 Goal

Store sensitive data (DB passwords, API keys)

---

## 🪜 Try This

1. Create secret
2. Use in deployment

---

## ✅ Solution

```bash id="wtt9vk"
kubectl create secret generic db-secret \
  --from-literal=DB_PASSWORD=supersecret
```

Use in Deployment:

```yaml id="2l8k4r"
env:
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: DB_PASSWORD
```

---

👉 NEVER hardcode secrets in YAML ❌

---

# 🧪 Exercise 13 — Resource Requests & Limits

## 🎯 Goal

Control CPU & memory (very important in real clusters)

---

## 🪜 Try This

Add limits to container

---

## ✅ Solution

```yaml id="3t0g9k"
resources:
  requests:
    memory: "128Mi"
    cpu: "200m"
  limits:
    memory: "256Mi"
    cpu: "500m"
```

---

👉 Why?

* Prevent one container from crashing entire system

---

# 🧪 Exercise 14 — Horizontal Pod Autoscaler (HPA)

## 🎯 Goal

Auto-scale based on load

---

## 🪜 Step 1 — Enable Metrics

```bash
minikube addons enable metrics-server
```

---

## 🪜 Step 2 — Create HPA

---

### ✅ Solution

```bash id="k0q2p6"
kubectl autoscale deployment nginx-deploy \
  --cpu-percent=50 \
  --min=2 \
  --max=10
```

Check:

```bash id="m6l9gk"
kubectl get hpa
```

---

👉 Kubernetes will scale pods automatically 🔥

---

# 🧪 Exercise 15 — Liveness & Readiness Probes

## 🎯 Goal

Detect broken apps automatically

---

## 🪜 Try This

Add health checks

---

## ✅ Solution

```yaml id="ojfj0j"
livenessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 5
```

---

👉 Difference:

* Liveness → restart container
* Readiness → stop sending traffic

---

# 🧪 Exercise 16 — Namespaces

## 🎯 Goal

Organize cluster (like environments)

---

## 🪜 Try This

Create namespace

---

## ✅ Solution

```bash id="m8mzzk"
kubectl create namespace dev

kubectl get namespaces
```

Run inside namespace:

```bash id="2ljxkm"
kubectl apply -f deployment.yaml -n dev
```

---

👉 Common setup:

* dev
* staging
* production

---

# 🧪 Exercise 17 — Full Production Architecture (Mini Project)

## 🎯 Goal

Combine everything into real system

---

## 🪜 Build This:

```
Ingress
   ↓
Service
   ↓
Deployment (Node App)
   ↓
MongoDB (with volume)
```

---

## ✅ Key Features You Must Include

* ✅ Ingress (domain routing)
* ✅ Secret (DB password)
* ✅ ConfigMap (app config)
* ✅ Volume (Mongo data)
* ✅ HPA (auto scaling)

---

# 🧠 Real Industry Architecture (What Companies Use)

```
Internet
   ↓
Ingress Controller
   ↓
Services
   ↓
Pods (Deployments)
   ↓
Database (StatefulSets)
```

---

# ⚠️ Common Mistakes (Interview Gold)

* ❌ Using NodePort in production
* ❌ Hardcoding secrets
* ❌ No resource limits
* ❌ Using Pods instead of Deployments
* ❌ No health checks

---



---
---
---
---
---
# Helm

Great—**Helm is where Kubernetes becomes practical at scale**.
Without Helm, managing 10–20 YAML files becomes painful. With Helm, you package everything cleanly.

Think of Helm like:
👉 **npm for Kubernetes**
👉 or **docker-compose for Kubernetes (but more powerful)**

---

# 🚀 PHASE 3 — Helm (Step-by-Step Hands-on)

We’ll go from zero → real project.

---

# 🧪 Exercise 1 — Install Helm

## 🎯 Goal

Get Helm CLI working

---

## 🪜 Try This

Check version

---

## ✅ Solution

```bash id="g8j7x2"
helm version
```

If not installed:

```bash id="u2n9s0"
# Linux
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

---

# 🧪 Exercise 2 — Create Your First Chart

## 🎯 Goal

Generate Helm project structure

---

## 🪜 Try This

Create a chart

---

## ✅ Solution

```bash id="l0v9rm"
helm create my-app
```

---

## 📁 Structure Explained

```
my-app/
 ├── templates/
 ├── values.yaml
 ├── Chart.yaml
```

---

👉 Important files:

* `values.yaml` → config
* `templates/` → Kubernetes YAML
* `Chart.yaml` → metadata

---

# 🧪 Exercise 3 — Install Chart

## 🎯 Goal

Deploy app using Helm

---

## 🪜 Try This

---

## ✅ Solution

```bash id="l1b9ck"
helm install my-release ./my-app
```

Check:

```bash id="1o5nfw"
kubectl get pods
```

---

👉 Helm created:

* Deployment
* Service
* etc.

---

# 🧪 Exercise 4 — Understand values.yaml (VERY IMPORTANT)

## 🎯 Goal

Make your app configurable

---

## 🪜 Try This

Change replica count

---

### `values.yaml`

```yaml
replicaCount: 3
```

---

### Template usage:

```yaml
replicas: {{ .Values.replicaCount }}
```

---

## ✅ Apply Changes

```bash id="7s3jlt"
helm upgrade my-release ./my-app
```

---

👉 This is Helm’s power 🔥

---

# 🧪 Exercise 5 — Dynamic Image Version

## 🎯 Goal

Change image without editing YAML

---

## 🪜 Try This

---

### `values.yaml`

```yaml
image:
  repository: nginx
  tag: "1.25"
```

---

### Template:

```yaml
image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
```

---

## ✅ Upgrade

```bash id="6s1c6c"
helm upgrade my-release ./my-app
```

---

# 🧪 Exercise 6 — Environment Variables via Helm

## 🎯 Goal

Pass env variables dynamically

---

## 🪜 Try This

---

### `values.yaml`

```yaml
env:
  APP_NAME: "MyHelmApp"
```

---

### Template:

```yaml
env:
  - name: APP_NAME
    value: "{{ .Values.env.APP_NAME }}"
```

---

---

# 🧪 Exercise 7 — Helm + ConfigMap

## 🎯 Goal

Manage config cleanly

---

## 🪜 Try This

---

### Template (`configmap.yaml`)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  APP_NAME: {{ .Values.env.APP_NAME }}
```

---

👉 Now config is centralized ✔️

---

# 🧪 Exercise 8 — Helm + Secrets

## 🎯 Goal

Secure sensitive values

---

## 🪜 Try This

---

### `values.yaml`

```yaml
secret:
  password: "mypassword"
```

---

### Template:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  password: {{ .Values.secret.password | b64enc }}
```

---

👉 Helm handles encoding 🔥

---

# 🧪 Exercise 9 — Helm Upgrade & Rollback (VERY IMPORTANT)

## 🎯 Goal

Safely deploy updates

---

## 🪜 Try This

---

## ✅ Solution

```bash id="hsmrmj"
helm upgrade my-release ./my-app
```

Check history:

```bash id="azffki"
helm history my-release
```

Rollback:

```bash id="b62a6p"
helm rollback my-release 1
```

---

👉 This is HUGE in production

---

# 🧪 Exercise 10 — Full Real Project (Helm Chart)

## 🎯 Goal

Convert your Node + Mongo app into Helm

---

## 🪜 You Should Build:

```
helm-chart/
 ├── templates/
 │    ├── deployment.yaml
 │    ├── service.yaml
 │    ├── configmap.yaml
 │    ├── secret.yaml
 │    ├── ingress.yaml
```

---

## ✅ Features to Include

* ✅ Deployment (Node app)
* ✅ Service
* ✅ Ingress
* ✅ ConfigMap
* ✅ Secret
* ✅ MongoDB connection via values.yaml

---

# 🧠 Real-World Helm Usage

In companies:

```id="v9mbpc"
Dev → changes values.yaml
     ↓
Helm upgrade
     ↓
Kubernetes updates app
```

---

# ⚠️ Common Mistakes

* ❌ Hardcoding values in templates
* ❌ Not using values.yaml properly
* ❌ Forgetting rollback
* ❌ Mixing env + secrets incorrectly

---

# 🚀 What You Can Do Now

At this point, you can:

* Package Kubernetes apps
* Reuse deployments
* Manage configs cleanly
* Deploy like real companies

---
---

👉 Docker → Kubernetes → Helm → **Cloud (AWS EKS)**

I’ll walk you through a **practical, end-to-end flow** to deploy your app on **Amazon EKS**.

---

# 🚀 PHASE 4 — Deploy to Cloud (AWS EKS)

We’ll build this pipeline:

```
Local App → Docker Image → AWS ECR → EKS Cluster → Helm Deploy
```

---

# 🧪 Step 0 — Prerequisites

You need:

* AWS account
* CLI tools:

  * `kubectl`
  * `helm`
  * AWS CLI
  * eksctl

---

# 🧪 Step 1 — Configure AWS

## 🎯 Goal

Connect your system to AWS

---

## 🪜 Try This

```bash
aws configure
```

Enter:

* Access Key
* Secret Key
* Region (e.g. `ap-south-1`)

---

# 🧪 Step 2 — Create EKS Cluster

## 🎯 Goal

Create managed Kubernetes cluster

---

## 🪜 Try This

---

## ✅ Solution

```bash
eksctl create cluster \
  --name my-cluster \
  --region ap-south-1 \
  --nodegroup-name my-nodes \
  --node-type t2.medium \
  --nodes 2
```

---

⏳ Takes ~10–15 minutes

---

## Verify

```bash
kubectl get nodes
```

---

👉 Now you have a real cloud cluster 🔥

---

# 🧪 Step 3 — Push Docker Image to AWS ECR

## 🎯 Goal

Store your app image in cloud registry

---

## 🪜 Step 1 — Create Repository

```bash
aws ecr create-repository --repository-name my-app
```

---

## 🪜 Step 2 — Login to ECR

```bash
aws ecr get-login-password | docker login \
--username AWS \
--password-stdin <your-account-id>.dkr.ecr.ap-south-1.amazonaws.com
```

---

## 🪜 Step 3 — Tag & Push Image

```bash
docker build -t my-app .

docker tag my-app:latest <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-app

docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-app
```

---

👉 Now your image is in AWS ✔️

---

# 🧪 Step 4 — Deploy App to EKS

## 🎯 Goal

Run your container in Kubernetes cloud

---

## 🪜 Try This

---

## ✅ Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-app
          ports:
            - containerPort: 3000
```

---

## Apply

```bash
kubectl apply -f deployment.yaml
```

---

# 🧪 Step 5 — Expose with LoadBalancer

## 🎯 Goal

Make app accessible from internet

---

## 🪜 Try This

---

## ✅ Solution

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 3000
```

---

```bash
kubectl apply -f service.yaml
```

---

## Get Public URL

```bash
kubectl get svc
```

👉 You’ll see **EXTERNAL-IP** 🌍

---

# 🧪 Step 6 — Use Helm (Production Style)

## 🎯 Goal

Deploy using Helm instead of raw YAML

---

## 🪜 Try This

---

## ✅ Solution

```bash
helm install my-app ./my-chart
```

Update image in `values.yaml`:

```yaml
image:
  repository: <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-app
  tag: latest
```

---

# 🧪 Step 7 — Add Ingress (Optional but Realistic)

Use:

* AWS Load Balancer Controller

---

👉 This gives:

* Domain-based routing
* HTTPS support

---

# 🧠 Real Production Architecture

```
User
 ↓
AWS Load Balancer
 ↓
Ingress Controller
 ↓
Kubernetes Services
 ↓
Pods (your app)
 ↓
Database (RDS / Mongo Atlas)
```

---

# ⚠️ Important Real-World Tips

### 💸 Cost Warning

* EKS is NOT free
* Always delete cluster after practice:

```bash
eksctl delete cluster --name my-cluster
```

---

### 🔐 Security Best Practices

* Use IAM roles (not root user)
* Store secrets in Kubernetes Secrets or AWS Secrets Manager

---

### 🚀 Performance

* Use auto-scaling (HPA)
* Use multiple AZs

---


Perfect. Now you’re stepping into **infra-as-code (IaC)**—this is how real teams manage cloud infrastructure.

👉 Instead of manually creating EKS clusters, you’ll define everything in code using **Terraform**.

---

# 🚀 PHASE 5 — Terraform + AWS EKS (Step-by-Step)

We’ll build this:

```id="nq4k96"
Terraform → AWS → EKS Cluster → Node Group → Ready for Kubernetes
```

---

# 🧪 Step 0 — Install Terraform

## 🎯 Goal

Set up Terraform CLI

---

## 🪜 Try This

```bash id="nqg4u2"
terraform -v
```

If not installed:

```bash id="x3g3rf"
# Linux
sudo apt-get update
sudo apt-get install terraform
```

---

# 🧪 Step 1 — Project Structure

## 🎯 Goal

Organize files like real projects

---

```id="g4y3xj"
terraform-eks/
 ├── main.tf
 ├── variables.tf
 ├── outputs.tf
```

---

# 🧪 Step 2 — AWS Provider

## 🎯 Goal

Tell Terraform to use AWS

---

### ✅ `main.tf`

```hcl id="53m1qy"
provider "aws" {
  region = "ap-south-1"
}
```

---

👉 Terraform now knows: “deploy to AWS”

---

# 🧪 Step 3 — Create VPC (Network)

## 🎯 Goal

Create networking for EKS

---

### ✅ Simple Version

```hcl id="g9g5fd"
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}
```

---

👉 In real setups, you’ll use modules (later)

---

# 🧪 Step 4 — Create EKS Cluster (Core Step)

## 🎯 Goal

Provision Kubernetes cluster

---

### ⚠️ Important

EKS setup manually is complex.
👉 We use official module:

---

### ✅ `main.tf` (Recommended way)

```hcl id="8qyzah"
module "eks" {
  source          = "terraform-aws-modules/eks/aws"
  cluster_name    = "my-cluster"
  cluster_version = "1.29"

  vpc_id     = "your-vpc-id"
  subnet_ids = ["subnet-1", "subnet-2"]

  eks_managed_node_groups = {
    default = {
      desired_size = 2
      max_size     = 3
      min_size     = 1

      instance_types = ["t2.medium"]
    }
  }
}
```

---

👉 This module handles:

* Control plane
* Node groups
* Networking

🔥 This is how companies actually do it.

---

# 🧪 Step 5 — Initialize Terraform

## 🎯 Goal

Download providers & modules

---

```bash id="9x6h1q"
terraform init
```

---

# 🧪 Step 6 — Plan (VERY IMPORTANT)

## 🎯 Goal

Preview changes before applying

---

```bash id="q4c51u"
terraform plan
```

---

👉 Shows what will be created ✔️

---

# 🧪 Step 7 — Apply (Create Infrastructure)

## 🎯 Goal

Actually create EKS cluster

---

```bash id="tqhzx2"
terraform apply
```

Type:

```id="kmc9sx"
yes
```

---

⏳ Takes ~15–20 minutes

---

# 🧪 Step 8 — Connect kubectl to EKS

## 🎯 Goal

Control your cluster

---

```bash id="p2mbbn"
aws eks update-kubeconfig --region ap-south-1 --name my-cluster
```

---

Check:

```bash id="c0hzvl"
kubectl get nodes
```

---

🔥 You now have a live EKS cluster created via code

---

# 🧪 Step 9 — Outputs (Useful Info)

## 🎯 Goal

Expose important values

---

### ✅ `outputs.tf`

```hcl id="0l1kqz"
output "cluster_name" {
  value = module.eks.cluster_name
}
```

---

Run:

```bash id="d4r2wz"
terraform output
```

---

# 🧪 Step 10 — Destroy (VERY IMPORTANT 💸)

## 🎯 Goal

Avoid AWS charges

---

```bash id="iyqjpr"
terraform destroy
```

---

👉 Always clean up!

---

# 🧠 Real-World Terraform Concepts

---

## 🔹 State File

Terraform keeps track in:

```id="i0ygj8"
terraform.tfstate
```

👉 Never lose this file ❗

---

## 🔹 Variables

### `variables.tf`

```hcl id="1d5yea"
variable "region" {
  default = "ap-south-1"
}
```

Use:

```hcl id="hs0fn4"
region = var.region
```

---

## 🔹 Modules (VERY IMPORTANT)

Instead of writing everything:

* Use reusable modules
* Like:

  * VPC module
  * EKS module

---

# ⚠️ Common Mistakes

* ❌ Hardcoding AWS credentials
* ❌ Not running `terraform plan`
* ❌ Forgetting `terraform destroy` (💸💸💸)
* ❌ Editing resources manually in AWS (drift issue)

---

# 🚀 What You Can Do Now

You now understand:

* Infrastructure as Code
* EKS provisioning via Terraform
* Modules
* State management
* Full cloud automation


---


You’re going to combine everything:

👉 **Terraform + Amazon EKS + Helm + GitHub Actions**

---

# 🚀 FINAL PROJECT — Full CI/CD + Cloud Deployment

## 🎯 Goal

Build a pipeline like this:

```id="j6r9eq"
Developer pushes code → GitHub Actions runs
        ↓
Build Docker image
        ↓
Push to AWS ECR
        ↓
Deploy to EKS using Helm
```

---

# 🧱 PROJECT STRUCTURE

```id="f2f5mt"
project/
 ├── app/                # Node app
 ├── helm-chart/         # Helm configs
 ├── terraform/          # EKS infra
 ├── .github/workflows/
 │     └── deploy.yml
```

---

# 🧪 STEP 1 — Terraform (Infra Setup)

👉 Already learned, but now structure it cleanly.

```id="hz6t5n"
terraform/
 ├── main.tf
 ├── variables.tf
 ├── outputs.tf
```

### ✅ Run

```bash id="bbmgpd"
terraform init
terraform apply
```

---

# 🧪 STEP 2 — Dockerize App

### Dockerfile

```Dockerfile id="cqv8o8"
FROM node:18

WORKDIR /app
COPY package.json .
RUN npm install

COPY . .

CMD ["node", "app.js"]
```

---

# 🧪 STEP 3 — Push to AWS ECR

Same as before, but CI will automate this.

---

# 🧪 STEP 4 — Helm Chart

Update `values.yaml`:

```yaml id="u85sp1"
image:
  repository: <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-app
  tag: latest
```

---

# 🧪 STEP 5 — GitHub Actions (CI/CD Core 🔥)

Create:

```id="8h8l0n"
.github/workflows/deploy.yml
```

---

## ✅ Full Pipeline

```yaml id="7s4k2q"
name: Deploy to EKS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_KEY }}
          aws-region: ap-south-1

      - name: Login to ECR
        run: |
          aws ecr get-login-password | docker login \
          --username AWS \
          --password-stdin ${{ secrets.AWS_ACCOUNT_ID }}.dkr.ecr.ap-south-1.amazonaws.com

      - name: Build Image
        run: docker build -t my-app .

      - name: Tag Image
        run: |
          docker tag my-app:latest \
          ${{ secrets.AWS_ACCOUNT_ID }}.dkr.ecr.ap-south-1.amazonaws.com/my-app

      - name: Push Image
        run: |
          docker push \
          ${{ secrets.AWS_ACCOUNT_ID }}.dkr.ecr.ap-south-1.amazonaws.com/my-app

      - name: Update kubeconfig
        run: |
          aws eks update-kubeconfig \
          --region ap-south-1 \
          --name my-cluster

      - name: Deploy with Helm
        run: |
          helm upgrade --install my-app ./helm-chart
```

---

# 🧪 STEP 6 — Add GitHub Secrets

Go to repo → Settings → Secrets

Add:

```id="9n8w4m"
AWS_ACCESS_KEY
AWS_SECRET_KEY
AWS_ACCOUNT_ID
```

---

# 🧪 STEP 7 — Push Code 🚀

```bash id="8ov3p0"
git add .
git commit -m "deploy"
git push origin main
```

---

👉 This triggers:

* Build
* Push
* Deploy automatically 🔥

---

# 🧪 STEP 8 — Verify Deployment

```bash id="tpqfha"
kubectl get pods
kubectl get svc
```

---

👉 Your app is LIVE 🌍

---

# 🧠 REAL INDUSTRY FLOW

```id="htns1o"
Code → GitHub
   ↓
CI/CD Pipeline
   ↓
Docker Image (ECR)
   ↓
Helm Deploy
   ↓
Kubernetes (EKS)
```

---

# ⚠️ Critical Real-World Practices

### 🔐 Security

* Never commit secrets
* Use IAM roles (better than access keys)

---

### 💸 Cost Control

* Stop EKS when not using
* Use small instances

---

### 🧪 Debugging

```bash id="sv93l2"
kubectl logs <pod>
kubectl describe pod <pod>
```

---

