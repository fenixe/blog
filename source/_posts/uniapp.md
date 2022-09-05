---
title: uniapp
date: 2022-04-09 15:39:49
categories:
- uniapp
tags:
- uniapp
---

# Base
## 基座
自定义调试基座是使用开发者申请的第三方SDK配置生成的基座应用，用于HBuilder/HBuilderX开发应用时实时在真机/模拟器上查看运行效果。（注：iOS仅支持真机运行自定义基座，不能使用xcode模拟器运行自定义基座）
基座：https://ask.dcloud.net.cn/article/35115
keystore生成：https://ask.dcloud.net.cn/article/35777
```
keytool -genkey -alias testalias -keyalg RSA -keysize 2048 -validity 36500 -keystore test.keystore
```

## 启动界面
android: 自定义启动图
ios：自定义storyboard


## 判断平台
html
``` html
<!-- #ifdef APP-PLUS -->
<view></view>
<!-- #endif -->

其他：MP-WEIXIN 
```

js
```js
if (process.env.UNI_PLATFORM === "h5") {}
if (process.env.UNI_PLATFORM === "app-plus") {}
if (process.env.UNI_PLATFORM === "mp-weixin") {}
if (process.env.UNI_PLATFORM === "mp-baidu") {}
```

## 内置方法
uni.hideKeyboard() //隐藏软键盘


## http request
```js
ureq =>
uni.request({
  url: '',
  method: 'GET',
  data: {},
  success: res => {},
  fail: () => {},
  complete: () => {}
});
```

## 路由
```js
uni.navigateTo({
  url: '../info/info?id=' + id
});
```

## page
```json
"path": "",
"style": {
  "app-plus":{
    "bounce": "none" // 将回弹属性关掉
  }
}
```

# Function
## Map
- [ ] 环境变量（最少三个环境）
- [ ] 公共样式
- [ ] http请求封装
- [ ] mock数据
- [ ] 状态栏适配
- [ ] 支付
- [ ] 基座
- [ ] 打包
- [ ] 热更新
- [ ] 上下架
- [ ] 网络模块（上传、下载、加密、重试、缓存、请求以及任务管理）
- [ ] 音视频模块（滤镜、播放、裁剪、合生、AV数据采集。图片处理、视频处理、渲染处理。）
- [ ] 基础框架（String、Array、Dictionary、TableView、Date等原生框架的补充）
- [ ] 数据（同步、读写、升级、清除缓存）
- [ ] 弹窗（toast、alert）
- [ ] 消息通知
- [ ] 消息通知

# 热更新
iOS的wgt更新肯定是违反apple政策的，注意事项：
- 审核期间请不要弹窗升级
- 升级完后尽量不要自行重启
- 尽量使用静默更新

## uni admin
项目名：uni-admin（不要改其他名字）
登录账号密码在：https://unicloud.dcloud.net.cn/
云数据库 - uni-id-users 库里面。忘记密码删除重新注册

## 