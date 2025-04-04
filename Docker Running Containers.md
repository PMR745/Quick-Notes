# Understanding Port Publishing in Docker

## What is Port Publishing?
Port publishing allows you to make a service running inside a Docker container accessible on the host machine or network. It maps a container's port to a host port.

## Syntax
```bash
docker run -p <host-port>:<container-port> <image>
```
- `<host-port>`: Port on the host machine.
- `<container-port>`: Port inside the container.

## Example
Suppose your container runs a web app on port `80` and you want to access it on port `8080` on the host:

```bash
docker run -p 8080:80 my-web-app
```
- Access the app at: `http://localhost:8080`

## Publishing Multiple Ports
You can publish multiple ports by using multiple `-p` flags:

```bash
docker run -p 8080:80 -p 8443:443 my-web-app
```

## Without Port Publishing
- The app inside the container will run but won't be accessible from the host.

## Port Publishing vs Exposing Ports
- **Exposing Ports**: Declares in the `Dockerfile` that a port is used (using `EXPOSE`), but it doesn't map it.
- **Publishing Ports**: Actively maps the container port to a host port using `-p`.

## Common Issues
1. **Port Already in Use**:
   - Another service is using the same port.
   - Solution: Use a different host port, e.g., `-p 8081:80`.

2. **Firewall Rules**:
   - Ensure your firewall allows traffic on the published port.

## Useful Commands
- **List Running Containers and Ports**:
  ```bash
  docker ps
  ```
  Output includes a `PORTS` column showing mappings like `0.0.0.0:8080->80/tcp`.

- **Inspect Container Network Configuration**:
  ```bash
  docker inspect <container-id>
  
