---
title: cocos
date: 2022-05-25 14:29:17
tags:
---

# Base
## debug
隐藏
cc.director.setDisplayStats(false)

## Sprite
### SizeMode
- CUSTOM 预设的尺寸
- TRIMMED 裁剪后的尺寸
- RAW 原图

## wechat
入口
- 微信小游戏：game.json
- 微信小程序：app.json

# 生命周期
https://docs.cocos.com/creator/manual/zh/scripting/life-cycle-callbacks.html

## onLoad

## start

## update

# 节点
## 自身节点
this.node

## 子节点
1.直接获取列表
this.node.children;

2.getChildByName
this.node.getChildByName("Cannon 01");

3.子节点的层次较深，可以使用cc.find
cc.find("Cannon 01/Barrel/SFX", this.node);

## 自身节点上的其他组件
{% asset_img other_component.png%}
1.使用函数 `getComponent`
```ts
var label = this.getComponent(cc.Label);
// this.node.getComponent(cc.Label)
var text = this.name + 'started';

// Change the text in Label Component
label.string = text;
```

2.函数可以直接传入一个类名（对用户定义的组件而言，类名就是脚本的文件名，并且区分大小写。）
```ts
var rotate = this.getComponent("SinRotate");
```