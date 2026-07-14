# Interactive Shell
Set proxy for **interactive shell processes**.

This does not affect system services, Ubuntu Desktop GUI apps, etc.

Add to `~/.bashrc`.
```shell
export HTTP_PROXY=http://<proxy-host>:<proxy-port>
export HTTPS_PROXY=http://<proxy-host>:<proxy-port>
export NO_PROXY=localhost,127.0.0.1

export http_proxy=http://<proxy-host>:<proxy-port>
export https_proxy=http://<proxy-host>:<proxy-port>
export no_proxy=localhost,127.0.0.1
```

Apply.
```shell
source ~/.bashrc
```

# `apt`
Set proxy for `apt`.

Create config.
```shell
sudo vim /etc/apt/apt.conf.d/95proxy
```

Add.
```
Acquire::http::Proxy "http://<proxy-host>:<proxy-port>/";
Acquire::https::Proxy "http://<proxy-host>:<proxy-port>/";
```

Priority: 
```
/etc/apt/apt.conf.d/95proxy > /etc/apt/apt.conf.d/10proxy > $HTTP_PROXY/$HTTPS_PROXY
```

`apt` reads config files in lexical order. `95proxy` is read later than `10proxy`, so it has higher priority.

# Docker Daemon
Set proxy for Docker daemon.  
[Docker Daemon](../Docker/Docker.md#Proxy##Docker%20Daemon)

# Ubuntu Desktop GUI
Set proxy for Ubuntu Desktop GUI apps.
```
Settings -> Network -> Network Proxy
```

This does not affect system services, interactive shell processes, etc.