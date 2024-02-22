---
slug: bitwarden-docker
title: bitwarden docker
authors:
  name: Liquor
  title: Docusaurus Core Team
  url: https://github.com/wgao19
  image_url: https://github.com/wgao19.png
tags: [bitwarden]
---

## 启动命令
```
docker run -d --rm --name bitwarden -p 8002:80 -p 3012:3012 -e SIGNUPS_ALLOWED=true -e WEB_VAULT_ENABLED=true -e DOMAIN=https://mmm.suole.me -v /opt/develop/bitwarden:/data vaultwarden/server:latest
```
