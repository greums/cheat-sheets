[Docker](https://docs.docker.com/) is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.

![](https://images.unsplash.com/photo-1504383633899-a17806f7e9ad?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1506&q=80)

## Install Docker Engine

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

## Configure Docker to start on boot

```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

## Configure remote access

If you want to grant access from a remote [Portainer service](https://github.com/greums/cheat-sheets/master/containerization/install-portainer-as-container.md), Docker daemon must be configured to listen on TCP port.
Create or update `/etc/docker/daemon.json`:
```bash
sudo nano /etc/docker/daemon.json
```
```json
{
  "tls": false,
  "hosts": ["unix:///var/run/docker.sock", "tcp://0.0.0.0:2376"]
}
```

Create a new file `/etc/systemd/system/docker.service.d/docker.conf` to fix conflict with default `systemd` configuration:
```bash
sudo mkdir /etc/systemd/system/docker.service.d/
sudo nano /etc/systemd/system/docker.service.d/docker.conf
```
```toml
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd
```

Then reload and restart service, and verify that Docker daemon is listening on the expected port:
```bash
sudo systemctl daemon-reload 
sudo systemctl restart docker.service
sudo netstat -lntp | grep dockerd
tcp    0    0 0.0.0.0:2376    0.0.0.0:*    LISTEN    327100/dockerd
```

> ⚠️ Binding to IP address without tls certificates is insecure and gives root access on this machine to everyone who has access to your network. 
