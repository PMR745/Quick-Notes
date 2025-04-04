

### Check Docker Version
```bash
docker --version
```

### View System Information
```bash
docker info
```

### List Available Commands
```bash
docker --help
```

---

## Images

### List Images
```bash
docker images
```

### Pull an Image
```bash
docker pull <image-name>:<tag>
```

### Build an Image
```bash
docker build -t <image-name>:<tag> .
```

### Remove an Image
```bash
docker rmi <image-id>
```

### Remove Unused Images
```bash
docker image prune
```

---

## Containers

### List Running Containers
```bash
docker ps
```

### List All Containers (Including Stopped)
```bash
docker ps -a
```

### Run a Container
```bash
docker run -d --name <container-name> -p <host-port>:<container-port> <image-name>:<tag>
```

### Stop a Running Container
```bash
docker stop <container-id>
```

### Restart a Container
```bash
docker restart <container-id>
```

### Remove a Container
```bash
docker rm <container-id>
```

### Remove All Stopped Containers
```bash
docker container prune
```

---

## Docker Compose

### Start Services
```bash
docker-compose up
```

### Start Services in Detached Mode
```bash
docker-compose up -d
```

### Stop Services
```bash
docker-compose down
```

### Restart Services
```bash
docker-compose restart
```

### Build Images Before Starting
```bash
docker-compose up --build
```

### View Logs
```bash
docker-compose logs
```

### View Logs of a Specific Service
```bash
docker-compose logs <service-name>
```

---

## Volumes

### List Volumes
```bash
docker volume ls
```

### Create a Volume
```bash
docker volume create <volume-name>
```

### Remove a Volume
```bash
docker volume rm <volume-name>
```

### Remove Unused Volumes
```bash
docker volume prune
```

---

## Networks

### List Networks
```bash
docker network ls
```

### Create a Network
```bash
docker network create <network-name>
```

### Connect a Container to a Network
```bash
docker network connect <network-name> <container-id>
```

### Disconnect a Container from a Network
```bash
docker network disconnect <network-name> <container-id>
```

### Remove a Network
```bash
docker network rm <network-name>
```

---

## Debugging and Logs

### View Container Logs
```bash
docker logs <container-id>
```

### View Real-Time Logs
```bash
docker logs -f <container-id>
```

### Access a Running Container’s Shell
```bash
docker exec -it <container-id> /bin/bash
```

### Inspect a Container
```bash
docker inspect <container-id>
```

### Monitor Resource Usage
```bash
docker stats
```

---

## Cleanup

### Remove All Stopped Containers, Unused Images, and Networks
```bash
docker system prune
```

### Remove All Data (Use with Caution!)
```bash
docker system prune -a
```

---

This cheatsheet covers the most common Docker CLI commands. Use `--help` with any command to get detailed options and usage information.
