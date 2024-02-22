---
title: MongoDB Docker 部署
---

### 拉取镜像
```
sudo docker pull mongo:4.0.4
```

### 启动容器
```
sudo docker run -p 27017:27017 -v ~/mongodb/data:/data/db --name docker_mongodb -d mongo:4.0.4
```