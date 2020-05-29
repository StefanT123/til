# Connect to a local network from inside a container

Once in a while, you may need your Docker host's IP address. For instance, you need to be able to connect to the host network from inside a Docker container to access your app or database running locally on the host. Debugging or reverse proxies running on your host are two additional example use-cases.
```yaml
version: '3.7'

services:
  app:
    image: your-app:latest
    ports:
      - "8080:8080"
    environment:
      SOME_VAR: http://${DOCKER_GATEWAY_HOST:-host.docker.internal}:3000
```

to automatize the iP (only get the first)
```bash
export DOCKER_GATEWAY_HOST="`hostname -I` | awk '{print $1}'  `"
```
