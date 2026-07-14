# Docker
Docker uses a **client-server** architecture. The **Docker client** communicates with the **Docker daemon** through a socket.

![](https://iot.samteck.net/wp-content/uploads/2018/10/vm-vs-docker.jpg)

Docker containers usually have better performance than virtual machines.
1. Docker containers have fewer abstraction layers than virtual machines. 
2. Docker containers share host machine’s kernel, virtual machines require separate Guest OS.

# Permission
## Docker Daemon
Docker CLI communicates with Docker daemon through a Unix socket:
```
/var/run/docker.sock
```

To run Docker CLI, your user needs permission to access this socket.

This socket usually has permissions like:
```
srw-rw---- 1 root docker ... /var/run/docker.sock
```

So to run Docker CLI, you need to either:
1. Use `sudo`.
2. Be root.
3. Be **in the docker group**.

To add your user to the docker group:
```shell
sudo usermod -aG docker $USER
```

Then log out and log back in, or run:
```shell
newgrp docker
```

The docker group is effectively root-equivalent.
## Root in a Container
Without user namespace remapping or rootless Docker, root (uid=0) in a container is root (uid=0) on the host, with restricted capabilities.

For example, in a bind mount, a file created by root (uid=0) in the container is also owned by root (uid=0) on the host.
## Rootless Docker
Rootless Docker means both Docker daemon and containers run without root privileges. 

With rootless Docker, a [user namespace](../Linux/Isolation.md#Namespace##User%20Namespace) is created for the processes inside the container. Root inside the container is not real root on the host.

# Proxy
## Docker Daemon
Create config.
```shell
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/proxy.conf
```

Add.
```
[Service]
Environment="HTTP_PROXY=http://<proxy-host>:<proxy-port>"
Environment="HTTPS_PROXY=http://<proxy-host>:<proxy-port>"
Environment="NO_PROXY=localhost,127.0.0.1"
```

Reload and restart docker.
```shell
sudo systemctl daemon-reload
sudo systemctl restart docker
```
## Docker Containers
```shell
docker run \
  -e HTTP_PROXY=http://<proxy_host>:<proxy_port> \
  -e HTTPS_PROXY=http://<proxy_host>:<proxy_port> \
  -e NO_PROXY=localhost,127.0.0.1 \
  <image>
```
This sets the container’s environment variables, it affects all processes started inside that container.