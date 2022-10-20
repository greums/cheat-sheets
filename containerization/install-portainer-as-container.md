[Portainer](https://www.portainer.io/) allow user to deploy, configure, troubleshoot and secure containers in minutes on Kubernetes, Docker, Swarm and Nomad in any cloud, data center or device.

![](https://images.unsplash.com/photo-1597334948330-38795f25d05d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1471&q=80)
📷 by [Dominik Lückmann](https://unsplash.com/@exdigy)

## Prerequisite

[Docker and Docker Compose](https://github.com/greums/cheat-sheets/blob/master/containerization/install-and-configure-docker.md) must be up and running before deploying Portainer. 

## Run Portainer container

```bash
docker run -d \
    --publish 8000:8000 \
    --publish 9443:9443 \
    --name portainer \
    --restart=always \
    --volume /var/run/docker.sock:/var/run/docker.sock \
    --volume ${HOME}/docker/portainer_data:/data \
    portainer/portainer-ce:latest
```

Once installation is complete, you can log into your Portainer Server instance by opening a web browser and going to https://localhost:9443. You will be presented with the initial setup page for Portainer Server.

Optionally, you can also publish port `9000` to expose an insecure HTTP connection.

## Auto-update running containers

If you want your containers to be always up-to-date, you can deploy Portainer alongside with [Watchtower](https://containrrr.dev/watchtower/).

Watchtower will pull down your new image, gracefully shut down your existing container and restart it with the same options that were used when it was deployed initially.

Create a new `docker-compose.yaml` with following services definition:
```yaml
version: "3.3"

services:
  portainer:
    container_name: portainer
    restart: unless-stopped
    ports:
      - "8000:8000"
      - "9443:9443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ${HOME}/docker/portainer_data:/data
    image: portainer/portainer-ce

  watchtower:
    container_name: watchtower
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    image: containrrr/watchtower
```

Then deploy and forget services:
```bash
docker-compose up --detach

[+] Running 2/2
 ⠿ Container watchtower Started
 ⠿ Container portainer  Started
```
