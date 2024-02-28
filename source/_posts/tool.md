---
title: tool
date: 2022-01-24 11:54:14
tags: vite
---


# css
Autoprefixer

# vite
## BG
在浏览器支持 ES 模块之前，JavaScript 并没有提供原生机制让开发者以模块化的方式进行开发。这也正是我们对 “打包” 这个概念熟悉的原因：使用工具抓取、处理并将我们的源码模块串联成可以在浏览器中运行的文件。

时过境迁，我们见证了诸如 webpack、Rollup 和 Parcel 等工具的变迁，它们极大地改善了前端开发者的开发体验。

然而，当我们开始构建越来越大型的应用时，需要处理的 JavaScript 代码量也呈指数级增长。包含数千个模块的大型项目相当普遍。基于 JavaScript 开发的工具就会开始遇到性能瓶颈：通常需要很长时间（甚至是几分钟！）才能启动开发服务器，即使使用模块热替换（HMR），文件修改后的效果也需要几秒钟才能在浏览器中反映出来。如此循环往复，迟钝的反馈会极大地影响开发者的开发效率和幸福感。

Vite 旨在利用生态系统中的新进展解决上述问题：浏览器开始原生支持 ES 模块，且越来越多 JavaScript 工具使用编译型语言编写。

# python
## Jupyter Notebook
pip install jupyter
jupyter notebook

# go
## 安装
https://go.dev/dl/

## 版本号
go version

# xxl-job
## 环境
Maven3+ 【mvn -v】
Jdk1.8+  【java -version】
Mysql5.7+

### Mysql版本
``` bash
mysql -u username -p
SELECT VERSION();
```

## 日志
----------- xxl-job job execute start -----------
----------- Param:
2024-02-27 02:00:00 [cn.eth.framework.logback.MdcLogAspect#jobAround]-[31]-[xxl-job, JobThread-25-1708970400043] mdc traceId: NC2ADPN1
2024-02-27 02:00:05 [com.xxl.job.core.thread.JobThread#run]-[179]-[xxl-job, JobThread-25-1708970400043] 
----------- xxl-job job execute end(finish) -----------


# powerjob



