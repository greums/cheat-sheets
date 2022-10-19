[Portainer](https://www.portainer.io/) allow user to deploy, configure, troubleshoot and secure containers in minutes on Kubernetes, Docker, Swarm and Nomad in any cloud, data center or device.

![](https://images.unsplash.com/photo-1597334948330-38795f25d05d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1471&q=80)

## Prerequisite

[Docker and Docker Compose](https://github.com/greums/cheat-sheets/master/containerization/install-and-configure-docker.md) must be up and running before deploying Portainer. 

## Run Portainer container

```bash
docker run -d \
    --publish 8000:8000 \
    --publish 9443:9443 \
    --name portainer \
    --restart=always \
    --volume /var/run/docker.sock:/var/run/docker.sock \
    --volume $HOME/docker/portainer_data:/data \
    portainer/portainer-ce:latest
```

Once installation is complete, you can log into your Portainer Server instance by opening a web browser and going to https://localhost:9443. You will be presented with the initial setup page for Portainer Server.

Optionally, you can also publish port `9000` to expose an insecure HTTP connection.
