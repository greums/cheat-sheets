# DevPi Server as local PyPi mirror

[DevPi Server](https://pypi.org/project/devpi-server/) is a local self-updating PyPi caching mirror which works with pip and easy_install. After files are first requested can work off-line and will try to re-check with pypi every 30 minutes by default.

![](https://images.unsplash.com/photo-1630086444439-97f3e422cc13?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1511&q=80)

📷 by [Rishabh Dharmani](https://unsplash.com/@rishabhdharmani)

## Install DevPi Server globally

```bash
sudo -H pip install devpi-server
sudo devpi-init
```

## Configure DevPi Server to start on boot

Create a new `systemctl` service:
```bash
sudo nano /etc/systemd/system/devpi.service
```
```toml
[Unit]
Description=Private pypi server by devpi-server
Requires=network-online.target
After=network-online.target

[Service]
Restart=always
ExecStart=/usr/local/bin/devpi-server --host localhost --port 3141
User=root

[Install]
WantedBy=multi-user.target
```

Reload configuration and start the service:
```bash
sudo systemctl daemon-reload
sudo systemctl enable devpi.service
sudo systemctl start devpi.service
```

## Configure pip to point to local mirror

Create or update your personal `pip` configuration:
```bash
mkdir ~/.config/pip/
nano ~/.config/pip/pip.conf
```
```toml
[global]
trusted-host = localhost
extra-index-url =  https://pypi.python.org

[install]
index-url = http://localhost:3141/root/pypi/+simple/

[search]
index = http://localhost:3141/root/pypi/
```

From now on, each `pip install` command will be resolved by DevPi Server. Requested packages will be served from cache, or fetched from PyPi if not found.
