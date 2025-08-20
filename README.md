# -AstrBot-NapCat-LLM-QQbot-

基于AstrBot和NapCat的可调用LLM的QQBot

本文参考网站:

AstrBot: [https://docs.astrbot.app/](https://docs.astrbot.app/)

NapCat: [https://napneko.github.io/](https://napneko.github.io/)

建议在vscode中进行操作

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