---
title: ubuntu 安装 docker 和 docker-compose
description: ubuntu 安装 docker 和 docker-compose
---

更新工具
```
sudo apt-get update
sudo apt-get upgrade
```

安装 docker
```
sudo apt-get install docker.io
```

启动docker
```
sudo service docker start
```

安装 docker-compose
```
curl -SL <https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-linux-x86_64> -o /usr/local/bin/docker-compose
```

赋予权限
```
sudo chmod +x /usr/local/bin/docker-compose
```

测试是否安装成功
```
docker-compose -v
```