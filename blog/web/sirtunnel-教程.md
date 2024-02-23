---
slug: SirTunnel-Tutorial
title: SirTunnel 教程
authors:
  name: Tony Garnock-Jones
  url: https://leastfixedpoint.com/tonyg/
tags: [web]
---

一个开源软件，只需要50行代码，就能建立一条隧道，将你的内网电脑可以被公网访问，这里有一篇教程。

https://eighty-twenty.org/2023/01/27/sirtunnel-personal-ngrok

新年快乐！

有时，我需要向世界公开一个开发网站或 Web 服务。过去，我曾使用 ngrok 来做到这一点，当然很久以前我构建了 ReverseHTTP，它位于同一个球场的某个地方，但我最近厌倦了事态，并决定看看是否有一些简单的东西我可以自己运行来完成这项工作。

我找到了安德斯·皮特曼（Anders Pitman）的SirTunnel：

https://github.com/anderspitman/SirTunnel

ngrok 的最小、自承载、0-config 替代方案。Caddy+OpenSSH+50行Python。

这真的非常简单。一个美丽的工程。从本质上讲，它编写了 Caddy 的 API 脚本，以动态添加和删除隧道。当您通过 SSH 连接到服务器时，您将调用该脚本，并且在 SSH 连接期间，服务器域的子域会通过 SSH 链接转发流量。

https://github.com/tonyg/SirTunnel

我已经为自己分叉了代码。到目前为止，我没有太大变化：脚本在启动时和退出时清理过时的注册，以防之前的连接以某种方式中断;我还添加了对转发到本地 TLS 服务的支持，以及可选的“不安全模式”来避免证书身份检查。

要让它在云中的 VM 上运行，请安装 Caddy（有一个 Debian bookworm 和 sid 的 caddy 软件包），然后禁用 systemd caddy 服务并启用该 caddy-api 服务：

```
apt install caddy
systemctl disable caddy
systemctl enable caddy-api
systemctl stop caddy
systemctl start caddy-api
```

为您的服务器设置通配符 DNS 记录 - 类似于 *.demo.example.com .每个隧道都将在 的子域上可用 demo.example.com 。

然后使用 API 上传一个简单的“全局”配置。这是我的：

```
{
  "apps": {
    "http": {
      "servers": {
        "default": {
          "logs": {},
          "listen": [":443"],
          "routes": []
        }
      }
    }
  }
}
```

通过将其放入文件 caddy_global.json 并运行来上传它

```
curl -L localhost:2019/load -H 'Content-Type: application/json' -d @caddy_global.json
```

然后，确保 SirTunnel 的 sirtunnel.py 脚本在服务器上的某个位置可供您的 SSH 用户帐户使用。

此时，要向全世界公开在端口 8443 上运行的本地开发服务，请执行以下操作：

```
ssh -t -R 8443:localhost:8443 YOURSERVER path/to/sirtunnel.py YOURAPP.demo.example.com 8443
```

我把它包在一个小脚本中，这样我就不必记住那个咒语的细节，但它足够简单，你每次都可以很容易地在终端中输入它。

非常感谢 Anders Pitman 提供了一个非常好的软件！