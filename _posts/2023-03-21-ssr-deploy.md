---
layout:       post
title:        "ssr部署"
author:       "ilyee"
header-style: text
catalog:      true
tags:
    - ssr
    - 部署
---

本文以`centos7`为例指导ssr服务器的部署和使用

## 安装git

`yum install git`

或者参考[git官方链接](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)安装git

## 配置ssr密钥

运行`ssh-keygen`，参数全选默认

```bash
cd ~/.ssh/
cat id_rsa.pub
```

复制`id_rsa.pub`公钥内容

在[这里](https://github.com/settings/keys)将复制的公钥配置给github

## 拉取ssr的github仓库

```bash
cd ~
# 这里也可以clone其他的ssr仓库，不一定是本文写的这个
git clone git@github.com:ToyoDAdoubiBackup/shadowsocksr.git
```

## 修改配置

```bash
cd ~/shadowsocksr/shadowsocks
vim config.json
```

下面是配置解析，具体的参数可以在客户端查看，参数和客户端保持一致即可

```json
{
    "server": "0.0.0.0", # ssr服务器地址，写0.0.0.0默认用本机IP
    "server_port": 2695, # ssr服务器端口，用未被占用的端口即可
    "local_address": "127.0.0.1", # 本机地址，写127.0.0.1即可
    "local_port": 1080, # 本机端口，用未被占用的端口即可

    "password": "test", # ssr客户端连接服务器的密码
    "method": "", # 加密方式
    "protocol": "", # 协议
    "protocol_param": "", # 协议参数，默认不写
    "obfs": "plain", # 混淆方式，plain为不混淆
    "obfs_param": "", # 混淆参数，默认不写
    "speed_limit_per_con": 0, # 单连接粒度的限流器，0为不限流
    "speed_limit_per_user": 0, # 单用户粒度的限流器，0为不限流

    # 下面参数为代理请求时的参数，默认不用更改
    "additional_ports" : {}, // only works under multi-user mode
    "additional_ports_only" : false, // only works under multi-user mode
    "timeout": 120,
    "udp_timeout": 60,
    "dns_ipv6": false,
    "connect_verbose_info": 0,
    "redirect": "",
    "fast_open": false
}
```

## 拉起服务

手动拉起

```bash
cd ~/shadowsocksr/shadowsocks
python server.py -c config.json
```

有输出的话则成功运行

`Centos`的话推荐用`systemctl`拉起

下面的文件放到`/usr/lib/systemd/system/shadowsocks.service`路径

```service
# /usr/lib/systemd/system/shadowsocks.service
[Unit]
Description=Shadowsocks Service

[Service]
ExecStart=/usr/bin/python3.6 /root/shadowsocksr/shadowsocks/server.py -c /root/shadowsocksr/shadowsocks/config.json
ExecReload=/usr/bin/python3.6 /root/shadowsocksr/shadowsocks/server.py -c /root/shadowsocksr/shadowsocks/config.json
Restart=always
RestartSec=5
LimitCORE=infinity
LimitNOFILE=100000
LimitNPROC=100000

[Install]
WantedBy=multi-user.target
```

执行

```bash
systemctl daemon-reload
systemctl start shadowsocks
```

服务便会随着系统启动自动拉起，并且异常自动重启，也会有日志追踪（用`journalctl -u shadowsocks`查看）

## 客户端安装&配置

可以从[这里](https://github.com/shadowsocksrr/shadowsocksr-csharp/releases)安装客户端，然后按照服务端的参数配置连接即可（注意客户端的服务器IP不能用0.0.0.0或127.0.0.1，需要用你购买的服务器的真实公网IP）
