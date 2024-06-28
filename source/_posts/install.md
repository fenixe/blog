---
title: 安装大全
date: 2020-02-23 17:47:57
categories:
- Tool
tags:
- Nodejs
- Yarn
---

# nodejs
Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。Node.js 的包管理器 npm，是全球最大的开源库生态系统。
### win
下载nodejs https://nodejs.org/zh-cn/

### linux
指定版本源
``` BASH
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```

安装
``` BASH
$ sudo apt install nodejs -y
```

如果安装比较慢，用代理
ubuntn 中测试是否开启代理
``` BASH
$ telnet 127.0.0.1 1080 // 1080是ssr端口

$ sudo vim /etc/apt/apt.conf.d/proxy.conf  #这个文件正常不存在，会新建一个
Acquire::http::Proxy "http://user:pwd@192.168.1.1:8080";

// 最后再删除
$ sudo rm /etc/apt/apt.conf.d/proxy.conf
```

## node_modules
### node-sass
[node-sass](https://github.com/sass/node-sass)
NodeJS  | Supported node-sass version | Node Module
--------|-----------------------------|------------
Node 20 | 9.0+                        | 115
Node 19 | 8.0+                        | 111
Node 18 | 8.0+                        | 108
Node 17 | 7.0+, <8.0                  | 102
Node 16 | 6.0+                        | 93
Node 15 | 5.0+, <7.0                  | 88
Node 14 | 4.14+, <9.0                 | 83
Node 13 | 4.13+, <5.0                 | 79
Node 12 | 4.12+, <8.0                 | 72
Node 11 | 4.10+, <5.0                 | 67
Node 10 | 4.9+, <6.0                  | 64
Node 8  | 4.5.3+, <5.0                | 57
Node <8 | <5.0                        | <57


# Yarn
### linux
[安装地址](https://yarn.bootcss.com/docs/install/#debian-stable)
``` BASH
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
// 此处要加 apt-get update; 不然安装的版本是0.33
$ sudo apt-get update && sudo apt-get install yarn -y
$ yarn --version
```

### init
默认初始化
yarn init -y 