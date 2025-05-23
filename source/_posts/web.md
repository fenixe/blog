---
title: web
date: 2020-05-27 10:41:51
tags:
---

# Base
Web服务器的作用说穿了就是：将某个主机上的资源映射为一个URL供外界访问。

# 一个普通网站访问的过程简单概括一下，对于我们普通的网站访问，涉及到的技术就是：
- 用户操作浏览器访问，浏览器向服务器发出一个 HTTP 请求；
- 服务器接收到 HTTP 请求，Web Server 进行相应的初步处理，使用服务器脚本生成页面；
- 服务器脚本（利用Web Framework）调用本地和客户端传来的数据，生成页面；
- Web Server 将生成的页面作为 HTTP 响应的 body，根据不同的处理结果生成 HTTP header，发回给客户端；
- 客户端（浏览器）接收到 HTTP 响应，通常第一个请求得到的 HTTP 响应的 body 里是 HTML 代码，于是对 HTML 代码开始解析；
- 解析过程中遇到引用的服务器上的资源（额外的 CSS、JS代码，图片、音视频，附件等），再向 Web Server 发送请求，Web Server 找到对应的文件，发送回来；
- 浏览器解析 HTML 包含的内容，用得到的 CSS 代码进行外观上的进一步渲染，JS 代码也可能会对外观进行一定的处理；
- 用户与页面交互（点击，悬停等等）时，JS 代码对此作出一定的反应，添加特效与动画；交互的过程中可能需要向服务器索取或提交额外的数据（局部的刷新，类似微博的新消息通知），一般不是跳转就是通过 JS 代码（响应某个动作或者定时）向 Web Server 发送请求，Web Server 再用服务器脚本进行处理（生成资源or写入数据之类的），把资源返回给客户端，客户端用得到的资源来实现动态效果或其他改变。

链接：https://www.zhihu.com/question/22689579/answer/22318058

# MEAN架构
神奇的MEAN架构，MongoDB做数据库，Express做 Web Framework，Angular 做前端的 JavaScript 框架，Node.js 用于编写 Web Server。神奇之处在于这几个东西的语言都是 JavaScript （MongoDB的实现不是，但与外界沟通用的语言是）。因为是比较新的架构，还有待时间的考验，不过被很多人（尤其是靠 JavaScript 吃饭的前端程序猿们）热切关注。

# Cache-Control
## 可缓存性
no-cache
在发布缓存副本之前，强制要求缓存把请求提交给原始服务器进行验证(协商缓存验证)。
no-store
缓存不应存储有关客户端请求或服务器响应的任何内容，即不使用任何缓存。

# DNS 解析
https://dash.cloudflare.com/


# 3.0
1、统一身份认证系统
2、数据确权与授权
3、隐私保护与抗审查
4、去中心化运行

## IPFS
Inter Planetary File System 星际文件系统

# HTTP
## 测试接口/请求接口
### get
https://httpbin.org/get

### post
https://httpbin.org/post


# 框架
每一个框架都是解决历史问题。

vue和react的瓶颈：项目庞大之后的卡顿问题
vue响应式数据过多。解决：组件控制响应式
两个树数据过大。解决：react16: Fiber tree

框架的迭代最后都是算法


npm -> yarn -> pnpm


# 区块链
## Base
一个区块链网络的核心是一个分布式账本，在这个账本中记录了网络中发生的所有交易信息。
交易一旦被添加进账本中，就无法被篡改。

### 火起来的原因
- 去中心化
- 投资理财

### 区块链行业
- 链圈
- 币圈

### 是什么
- 区块链是一个分布式网络；
- 区块链可以帮助多个节点达成共识去记录和 Token 相关的事情；
- 区块链可以帮助所有人无门槛地构建属于自己的小经济系统。

### 智能合约
为了持续的进行信息的更新，以及对账本进行管理（写入交易，进行查询等），区块链网络引入了智能合约来实现对账本的访问和控制。
智能合约不仅仅可用于在区块链网络中打包信息，它们也可以被用于自动的执行由参与者定义的特定交易操作。（例如收获付款）

### 共识
保持网络中所有账本交易的同步流程，就是共识。共识保证了账本只会在交易双方都确认后才进行更新。同时在账本更新时，交易双方能够在账本中的相同位置，更新一个相同的交易信息。

## 共识机制
遇到的问题
- 谁有权利；
- 作弊问题。
### 入门型共识机制
PoW （Proof of Work）工作量证明可以解决上述的两个问题，

## 公有链 & 联盟链
公链：任何人都可以随时进入
联盟链（许可链）：这个区块链具有准入许可

## 区块链在技术上的7个特征
1、区块链的存储基于分布式数据库；
2、数据库是区块链的数据载体，区块链是交易的业务逻辑载体；
3、区块链按时间序列化区块数据，整个网络有一个最终确定状态；
4、区块链只对添加有效，对其他操作无效；
5、交易基于非对称加密的公私钥验证；
6、区块链网络要求拜占庭将军容错；
7、共识算法能够“解决”双花问题。

## 区块链核心技术组成
1、P2P网络协议
2、分布式一致性算法（共识机制）
3、加密签名算法
4、账户与存储模型

### P2P网络
- P2P网络协议
- 区块链的P2P技术
- 网络连接与拓扑结构
- 节点发现
- 黑名单与长连接
- 局域网穿透
- 节点交互协议

# Hyperledger Fabric
区块链是一个共享的，通过智能合约更新的多副本交易系统，同时这个系统通过协作共识机制保证了网络中所有账本副本的同步。
https://blog.csdn.net/xiaohanshasha/article/details/122574705

## 部署生产网络
https://hyperledger-fabric.readthedocs.io/en/release-2.3/deployment_guide_overview.html

## 问题
报错：osnadmin: error: parsing arguments: unknown long flag '--channel-id'
解决办法：
修改：将./test-network/script/createChannel.sh第40行长标志改为osnadmin channel join --channelID


# 专业术语
## 拨测
在网络通信中，"拨测"通常指的是通过模拟用户访问的方式，对网络服务进行测试和监控。这种测试可以帮助识别网络性能问题、服务可用性以及响应时间等。拨测通常用于：

- 监控服务可用性：确保服务在不同时间和地点都能正常访问。
- 性能测试：测量响应时间和数据传输速度。
- 故障排查：通过定期测试，及时发现和解决潜在的网络问题。

https://boce.aliyun.com/detect/http