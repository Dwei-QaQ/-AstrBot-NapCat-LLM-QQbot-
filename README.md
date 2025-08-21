# -AstrBot-NapCat-LLM-QQbot-

基于AstrBot和NapCat的可调用LLM的QQBot

本文参考网站:

AstrBot: [https://docs.astrbot.app/](https://docs.astrbot.app/)

NapCat: [https://napneko.github.io/](https://napneko.github.io/)

环境为Ubuntu 20.04，建议在vscode中进行操作

## 1. 安装Natpat并启动

使用docker的办法

先配置docker，使用 apt 安装软件包,在命令行输入

```bash
sudo apt-get update
sudo apt-get install ./docker-desktop-amd64.deb
```

使用以下命令：

```bash
curl -o napcat.sh https://raw.githubusercontent.com/NapNeko/napcat-linux-installer/refs/heads/main/install.sh && sudo bash napcat.sh
```

使用以下命令启动：

```bash
sudo bash ./launcher.sh 
```

会出现二维码，扫码登录

然后就可以看到转发端口及其地址，如

```bash
127.0.0.1:6100
```

点击浏览器访问

输入token，点击登录

token可通过查找config文件获得,如：

```bash
{
    "host": "0.0.0.0",
    "port": 6099,
    "token": "your_token_here",
    "loginRate": 10,
    "autoLoginAccount": "",
    ...
}
```

这个时候就可以接收消息日志了

## 2. 安装AstrBot并启动

使用docker的办法进行部署

使用以下命令拉取镜像：

```bash
sudo docker run -itd -p 6180-6200:6180-6200 -p 11451:11451 -v $PWD/data:/AstrBot/data -v /etc/localtime:/etc/localtime:ro -v /etc/timezone:/etc/timezone:ro --name astrbot m.daocloud.io/docker.io/soulter/astrbot:latest
```

6196是 QQ 官方 API(Webhook) HTTP callback server 默认端口

11451是Gewechat callback HTTP server 默认端口

通过以下命令查看 AstrBot 的日志：

```bash
sudo docker logs -f astrbot
```

通过浏览器访问 `http://localhost:6185` 进行查看

## 3. 连接到 AstrBot

### 在 AstrBot 配置 aiocqhttp

1. 进入 AstrBot 的管理面板

2. 击左边栏 消息平台

3. 然后在右边的界面中，点击 + 新增适配器

4. 选择 aiocqhttp(OneBotv11)

弹出的配置项填写：

配置项填写：

- ID(id)：随意填写，用于区分不同的消息平台实例。

- 启用(enable): 勾选。

- 反向 WebSocket 主机地址：请填写你的机器的 IP 地址。一般情况下请直接填写 0.0.0.0

- 反向 WebSocket 端口：填写一个端口，例如 6199。

点击 保存。

### 配置管理员

填写完毕后，进入 配置 页，点击 其他配置 选项卡，找到 管理员 ID，填写你的 QQ 号（不是机器人的 QQ 号）。

切记点击右下角 保存，AstrBot 重启并会应用配置。

### 在 NapCatQQ 中添加 WebSocket 客户端

切换回 NapCatQQ 的管理面板，点击 网络配置->新建->WebSockets客户端。

在新弹出的窗口中：

- 勾选 启用。

- URL 填写 ws://宿主机IP:端口/ws。如 ws://localhost:6199/ws或ws://127.0.0.1:6199/ws。

- 消息格式：Array

- 心跳间隔: 5000

- 重连间隔: 5000

点击 保存。

前往 AstrBot WebUI 控制台，如果出现 aiocqhttp(OneBot v11) 适配器已连接。 相关蓝色的日志，说明连接成功。

此时，你的 AstrBot 和 NapCatQQ 应该已经连接成功。使用 私聊 的方式在 QQ 对机器人发送 /help 以检查是否连接成功。