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

就是一个壳子，包含manifest里面的所有设置，还有HBuilderX版本

### 云打包模式
1. 安心打包，不会上传开发者证书代码
2. 传统云打包，没有mac需要打ios包的开发者，代码和证书上传到DCloud的mac打包服务器
## 两套开发模式
1. HBuilderX 可视化界面
2. cli创建项目

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

### 默认路由
pages.json
```json
"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		{
			"path": "pages/new/home",
			"style": {
				"navigationBarTitleText": "购买好药"
			}
		},
]
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

## css
### 不支持的选择器
非H5端不支持*选择器；
body的元素选择器请改为page，同样，div和ul和li等改为view、span和font改为text、a改为navigator、img改为image...

### scoped
非H5端默认并未启用 scoped，如需要隔离组件样式可以在 style 标签增加 scoped 属性，H5端为了隔离页面间的样式默认启用了 scoped

## 小程序
小程序要求连接的网址都要配白名单

- 不能使用浏览器自带对象，document、window、localstorage、cookie等
- 不同的端，每个平台的专有api，比如wx.、plus.等api可以分别在微信下和app下使用
- 推荐使用flex布局模型，支持多平台
- 位置坐标系统一为国测局坐标系gcj02，这种坐标系可以被多端支持

## 跨域
跨域是浏览器的专用概念
做App、小程序等非H5平台，是不涉及跨域问题
iOS的 wkWebview ，会产生跨域

## 跨端
组件内（页面除外）不支持 onLoad、onShow 等页面生命周期。

## 分包
小游戏
小程序 工具 vendor.js过大

## 全局变量
赋值：getApp().globalData.text = 'test'
取值：console.log(getApp().globalData.text) // 'test'

## vuex
main.js 挂载 Vuex
import store from './store'  
Vue.prototype.$store = store

## 存储
uni.storage的键值对存储，全端支持。

## 升级
HBuilderX升级后，其自带的app运行基座、uni-app编译器、云打包配套引擎会同步升级。但在开发者使用cli创建项目、使用自定义基座、使用5+sdk离线打包时，就需要手动维护版本更新。

小程序，提交代码到小程序后台
app，ios去appstore，android直接下载apk，只要包名和证书不变，就可以覆盖安装。

App升级，也可使用uniCloud。

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
- [ ] 导航栏 https://ask.dcloud.net.cn/article/34921

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

# HTML5+
HTML5+标准规范，是对HTML5的一种扩展，扩展后的HTML5可以达到原生的功能和体验。


