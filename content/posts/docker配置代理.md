+++
title = "Docker proxy"
date = 2025-08-20
categories = ["Docker"]
tags = ["Docker","Linux"]

+++

> 内容来自ChatGPT

好 👍 如果要让 **Docker 全局走代理**，要给 **Docker Daemon 配置代理**。一般分两步：

------

## 🔧 1. 创建代理配置文件

首先新建目录（如果不存在）：

```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
```

然后创建配置文件：

```bash
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```

写入内容（假设代理是 `127.0.0.1:7890`，改成你自己的）：

```ini
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:7890"
Environment="HTTPS_PROXY=http://127.0.0.1:7890"
Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.somecorporation.com"
```

------

## 🔧 2. 让配置生效

保存后执行：

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl restart docker
```

------

## 🔧 3. 验证

执行：

```bash
systemctl show --property=Environment docker
```

如果能看到刚才设置的 `HTTP_PROXY` 和 `HTTPS_PROXY`，说明生效了。

------

## 🔧 4. 注意事项

- 如果你用的是 **Clash / V2Ray / Surge 等客户端**，本地代理通常是 `127.0.0.1:7890`（http），如果是 socks5，需要写成：

  ```ini
  Environment="HTTP_PROXY=socks5://127.0.0.1:7890"
  ```

- `NO_PROXY` 很重要，否则连 `localhost` 也会走代理，可能导致容器访问宿主机时出问题。

