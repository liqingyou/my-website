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

## 设置密码

### 進入容器
```
docker exec -it docker_mongodb /bin/bash
mongo admin
db.createUser({user: "用户名", pwd: "密码", roles: [{role: "dbAdmin", db: "admin"}]})
db.auth('admin', 'admin')
```

### 链接url
```
mongodb://用户名:密码@db:27017/api-mock?authSource=admin
url中特殊符号需要转义
```

#### 参考地址
https://tsejx.github.io/devops-guidebook/deploy/docker/mongodb/
