# Docker Cheat Sheet

## 🔹 Basic Commands
```sh
# Check Docker version
docker --version

# Show system-wide information
docker info

# List all running containers
docker ps

# List all containers (including stopped ones)
docker ps -a

# List all images
docker images

# List all volumes
docker volume ls
```

## 🔹 Container Management
```sh
# Run a container interactively
docker run -it <image> bash

# Run a container in detached mode
docker run -d <image>

# Start a stopped container
docker start <container_id>

# Stop a running container
docker stop <container_id>

# Restart a container
docker restart <container_id>

# Remove a container
docker rm <container_id>

# Remove all stopped containers
docker container prune
```

## 🔹 Image Management
```sh
# Pull an image from Docker Hub
docker pull <image>

# Build an image from a Dockerfile
docker build -t <image_name> .

# Remove an image
docker rmi <image_id>

# Remove all unused images
docker image prune -a
```

## 🔹 Networking
```sh
# List networks
docker network ls

# Create a new network
docker network create <network_name>

# Connect a container to a network
docker network connect <network_name> <container_id>

# Disconnect a container from a network
docker network disconnect <network_name> <container_id>
```

## 🔹 Volumes & Persistent Storage
```sh
# Create a volume
docker volume create <volume_name>

# Mount a volume when running a container
docker run -v <volume_name>:/data <image>

# Remove a volume
docker volume rm <volume_name>

# Remove all unused volumes
docker volume prune
```

## 🔹 Docker Compose
```sh
# Start services using docker-compose
docker-compose up

# Start services in detached mode
docker-compose up -d

# Stop services
docker-compose down

# Restart services
docker-compose restart
```

## 🔹 Logs & Debugging
```sh
# View logs of a container
docker logs <container_id>

# Follow logs in real-time
docker logs -f <container_id>

# Check container stats (CPU, memory, network usage)
docker stats
```

## 🔹 Executing Commands in a Running Container
```sh
# Open a shell inside a running container
docker exec -it <container_id> bash

# Run a command inside a container
docker exec <container_id> <command>
```

## 🔹 Cleaning Up
```sh
# Remove all stopped containers, networks, and dangling images
docker system prune

# Remove everything (containers, networks, images, volumes)
docker system prune -a --volumes
```

## 🔹 Multi-Stage Builds (Optimizing Image Size)
```Dockerfile
# Example multi-stage Dockerfile
FROM node:16 as build
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]
```

## 🔹 Docker BuildKit (Faster Builds)
```sh
# Enable BuildKit for improved performance
export DOCKER_BUILDKIT=1

# Build an image using BuildKit
docker build --progress=plain -t <image_name> .
```

## 🔹 Docker Swarm (Container Orchestration)
```sh
# Initialize a Swarm cluster
docker swarm init

# Create a service in Swarm
docker service create --name my_service -p 80:80 nginx

# List all services
docker service ls

# Scale a service to 3 replicas
docker service scale my_service=3

# Remove a service
docker service rm my_service
```

## 🔹 Kubernetes with Docker
```sh
# Enable Kubernetes in Docker Desktop
# Start a Kubernetes deployment
docker run --name k8s -d -p 6443:6443 k8s.gcr.io/kube-apiserver:v1.23.0

# Deploy an application using kubectl
kubectl apply -f deployment.yaml

# List running pods
kubectl get pods
```

## 🔹 Advanced Security
```sh
# Scan an image for vulnerabilities
docker scan <image>

# Run a container with read-only filesystem
docker run --read-only <image>

# Run a container with a limited user
docker run -u 1001 <image>

# Sign an image for integrity verification
docker trust sign <image>
```

## 🔹 Performance Tuning
```sh
# Limit container memory usage
docker run -m 512m <image>

# Limit CPU usage
docker run --cpus="1.5" <image>

# Check container performance metrics
docker stats
```

## 🔹 Docker Storage Drivers
```sh
# Check current storage driver
docker info | grep "Storage Driver"

# Change storage driver (example: overlay2)
DOCKER_OPTS="--storage-driver=overlay2"
```

## 🔹 Docker Plugins (Extend Functionality)
```sh
# List available plugins
docker plugin ls

# Install a plugin
docker plugin install <plugin_name>

# Enable a plugin
docker plugin enable <plugin_name>
```

## 🔹 Docker Enterprise Features
```sh
# Enable Docker Enterprise security features
docker security enable

# Use Content Trust to verify image integrity
export DOCKER_CONTENT_TRUST=1
```

Now, this cheat sheet includes everything about **Docker**, from basics to advanced enterprise-level features. 🚀
