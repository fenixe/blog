---
title: coding
date: 2020-03-02 13:02:23
categories:
- code
tags:
- code
---

# Base
## 存储单位
在计算机科学中，“字节”是数据存储的基本单位，且其大小是标准的：一个字节由8位（bits）组成。因此，在基本层面上，计算机里只有一种字节（byte），其由8个二进制位组成。
然而，描述数据大小时，我们通常会使用更大的单位来表示较大的数据量。这些单位是基于字节的，并且按照一定的规模来递增，通常是按照1024的规模来递增，因为计算机是按照二进制来运行的。以下是一些常见的单位及其与字节之间的关系：
1 Byte (B) = 8 bits (比特)
1 Kilobyte (KB) = 1024 Bytes
1 Megabyte (MB) = 1024 Kilobytes
1 Gigabyte (GB) = 1024 Megabytes
1 Terabyte (TB) = 1024 Gigabytes
1 Petabyte (PB) = 1024 Terabytes
1 Exabyte (EB) = 1024 Petabytes
1 Zettabyte (ZB) = 1024 Exabytes
1 Yottabyte (YB) = 1024 Zettabytes
注意，有两个标准被使用来描述数据大小：IEC（国际电工委员会）和SI（国际单位制）。IEC使用1024作为递增基数，如上所示，而SI使用1000作为递增基数。这导致了一些混淆，因为硬盘制造商通常使用SI标准来标记容量，而操作系统则可能使用IEC标准。
为了消除歧义，IEC引入了一些特殊的单位，比如用“Kibibyte (KiB)”代替“Kilobyte (KB)”表示1024字节，但在实际使用中，“Kilobyte”这个词常常用来表示1024字节。

### 10MB转换为字节
使用最常见的定义，也就是以1024为基数（根据IEC标准）：
1 Megabyte (MB) = 1,024 Kilobytes (KB)1 Kilobyte (KB) = 1,024 Bytes (B)
所以，10 Megabytes (MB) = 10 * 1,024 * 1,024 = 10,485,760 Bytes
因此，10MB转换为字节就是10,485,760字节。

## 处理器架构
amd64 强调高性能和向后兼容性，适用于桌面和服务器市场；
arm64 强调低功耗和高效性，适用于移动设备和嵌入式系统。
### amd64（x86-64）
别名：x86-64、x64、Intel 64、EM64T

### arm64（AArch64）
别名：AArch64、ARMv8-A

### 区别
主要区别
指令集架构：

amd64：基于复杂指令集计算（CISC），扩展自x86架构。
arm64：基于精简指令集计算（RISC），全新设计的64位指令集。
功耗和性能：

amd64：通常功耗较高，但在高性能计算和多线程任务中表现优异。
arm64：功耗较低，适合移动设备和嵌入式系统，同时在性能上也有不错的表现。
应用场景：

amd64：主要用于桌面电脑、服务器和高性能计算。
arm64：主要用于移动设备、嵌入式系统、物联网设备以及一些服务器应用。
兼容性：

amd64：向后兼容x86（32位）软件，提供平滑的过渡路径。
arm64：向后兼容ARMv7（32位）软件，但需要在不同模式下运行。

## 专业词
### 访问控制
access key 访问密钥（类似于用户名）
access key secret 与access key配对的密钥，用于验证用户或应用程序的身份。它类似于密码或私钥，必须保密。（类似于密码）

Public Key（公钥）
Private Key（私钥）

### 签名
sign，signature

### 随机
random 随机
nonce 随机数

### 时间戳
timestamp

### 第三方
third

## 加密方式
下午好!很高兴和您交流。关于您提到的AES/CBC/PKCS7加密,我可以为您详细解释一下:

1. AES (Advanced Encryption Standard):
   这是一种对称加密算法,被广泛用于保护电子数据。AES支持128位、192位和256位密钥长度。

2. CBC (Cipher Block Chaining):
   这是一种操作模式,用于将加密算法应用于较长的消息。在CBC模式中,每个明文块在加密之前会与前一个密文块进行异或操作,这增加了加密的安全性。

3. PKCS7 (Public Key Cryptography Standards #7):
   这是一种填充方案,用于确保待加密的数据块长度符合块加密算法的要求。PKCS7填充会在数据末尾添加一些字节,使其长度成为块大小的整数倍。

综合起来,"AES/CBC/PKCS7"表示:
- 使用AES算法进行加密
- 采用CBC模式处理数据块
- 使用PKCS7方法进行填充
这种组合提供了较高的安全性,适用于多种应用场景,如保护敏感数据传输、文件加密等。

### hex
十六进制（hex）：一种基数为16的数字系统，使用0-9和A-F表示。
字节（byte）：由8个二进制位组成，可以表示0到255的值。在十六进制中，一个字节可以表示为两个十六进制字符。

## 项目环境
dev，uat，prod

## 变量名
```java
String xApiUrl = "https://www.baidu.com/api/x";
```

# 调试
获取授权url
Method: post
URL: http://d-gamenc.ethicall.cn/game/nc/auth/oauth
Params: {
	redirectUrl: "d-gamenc.ethicall.cn/wx.html#/auth?fr=http%3A%2F%2Flocalhost%3A7457%2F"
}
Response: {
		code: "500"
}

## 线上版本查看
前端: dist文件
Java: 拿包对下

# 编码

调试
重构
迭代

版本管理




# 编码规范

## 文件命名
文件（目录）名全部使用小写字母和连词线（all-lowercase-with-dashes）
单个.js 文件可以用驼峰
首字母一定要小写*
[阮一峰](https://www.ruanyifeng.com/blog/2017/02/filename-should-be-lowercase.html)
文件名全部使用小写字母和连词线（all-lowercase-with-dashes），是一种值得推广的正确做法。

### 可移植性
- Linux系统大小写敏感
- Windows系统和Mac系统，大小写不敏感

### 易读性
小写文件名通常比大写文件名更易读，比如`accessibility.txt`就比`ACCESSIBILITY.TXT`易读。

### 易用性
系统文件 大写
用户文件 小写

### 便捷性
文件名全部小写，还有利于命令行操作。比如，某些命令可以不使用`-i`参数了

## Angular guide
[编码规范](https://angular.io/guide/styleguide)
[Angular代码风格](https://www.jianshu.com/p/90cc5899c40c)

# 设计
设计的重要性
架构和规划：

设计阶段决定了系统的整体架构和模块划分，确保系统具有良好的可扩展性、可维护性和性能。
通过设计，可以提前识别和解决潜在的问题，避免在实现阶段出现重大变更。
需求分析和确认：

设计阶段是将需求转化为技术实现的关键步骤。通过详细的设计文档和模型，可以确保所有利益相关者对系统的功能和行为有一致的理解。
降低风险和成本：

良好的设计可以减少开发过程中的返工和修复成本。通过设计评审和原型验证，可以在早期发现并解决问题，降低项目风险。
提高开发效率：

设计提供了明确的开发指南和规范，使开发团队能够更高效地进行编码和测试，减少沟通成本和误解。

# 快捷键
## css
w400 => width: 400px;

## html
ul>li

# other
中国人的探索精神没有
{% asset_img explore.png%}

# 指导
## 页面
{% asset_img coding.png%}
我写的太乱了，看不明白，不能理解
在service中处理 数据
时间的话 util 工具，在视图层处理 
不利于别人复用维护

# 待看
https://github.com/TheWindRises-2/coco-message

# 如何提升自己架构设计的感觉？

代码的可读性、扩展性、完善自己的加速框架（知识库）。
勤于思考，在下笔之前，一定要做结构、图表分析。
多沟通，无论是自己的组员还是自己的上司，或者是设计还是产品，往往灵感一触即发。
多读第三方的源码，思考为什么作者这样设计，这样做有什么好处和坏处。
做垂直领域，完善自己的技术壁垒
做宽度领域，多看一些Python、Go、Swift、Java、JS、PHP等语言，见得多才能更全面的分析。

