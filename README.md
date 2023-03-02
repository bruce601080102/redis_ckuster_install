# Redis cluster

```bash
vim etc/docker/daemon.json
```

```bash
{
  "insecure-registries":["59.125.100.235:5000","10.140.0.3:5000"],
  "log-driver": "json-file",
  "log-opts": {"max-size": "10m", "max-file": "2"}
}
```

```bash
systemctl restart docker
```

### Post-installation steps for Linux 設定不用root 模式下, 操作Docker

```bash
$sudo groupadd docker
$sudo usermod -aG docker $USER
$newgrp docker
```

### 安裝redis-cli

```bash
curl -fsSL [https://packages.redis.io/gpg](https://packages.redis.io/gpg) | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
```

```bash
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
```

```bash
apt-get update
apt-get install redis

redis-cli --cluster create 192.168.10.112:7001 192.168.10.112:7002 192.168.10.112:7003 192.168.10.112:7004 192.168.10.112:7005 192.168.10.112:7006 --cluster-replicas 1 -a pass.123
```