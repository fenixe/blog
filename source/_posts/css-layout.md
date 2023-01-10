---
title: flex
date: 2020-06-20 10:41:08
categroces:
- CSS
tags:
- CSS
- Flex
- Grid
---


# Flex
## 是什么
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

## 为什么
传统布局，基于盒状模型，依赖 display 属性 + position属性 + float属性 。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。
所以浏览器都支持。


## 基本概念
采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。
`<% asset_img flex.png %>`

## 设置 Flex 布局。
### 块元素
``` css
.box {
  display: flex;
}
```

### 行内元素
``` css
.box{
  display: inline-flex;
}
```

注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。


## 容器的属性
flex-direction
flex-wrap
flex-flow
justify-content
align-items
align-content

### flex-direction属性
flex-direction属性决定主轴的方向（即项目的排列方向）。

row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。

## flex-wrap属性
nowrap（默认）：不换行。
wrap：换行，第一行在上方。
wrap-reverse：换行，第一行在下方。

### flex-flow
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

### justify-content属性
justify-content属性定义了项目在主轴上的对齐方式。

flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-content
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。

### align-items
items值flex子项们，相对于flex容器在垂直方向上的对齐方式
align-items: stretch | flex-start | flex-end | center | baseline;

## 项目的属性
### order
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

### flex-grow
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### flex-shrink
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

### flex-basis属性
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

### flex属性
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

### align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。


# Grid
布局创建
```css
div{
  display: grid;
}
```
此时该div就是“grid容器”，其子元素称为“grid子项”。

## 作用在grid上的css属性
### grid-template-columns和grid-template-rows
```css
.container {
    grid-template-columns: 80px auto 100px;
    grid-template-rows: 25% 100px auto 60px;
}
```
{% asset_img template.png %}

### grid-template-areas
给网格划分区域
```html
.container {
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    grid-template-areas: 
        "葡萄 葡萄 葡萄"
        "龙虾 养鱼 养鱼"
        "龙虾 养鱼 养鱼"
        "西瓜 西瓜 西瓜";
}
.putao { grid-area: 葡萄; }
.longxia { grid-area: 龙虾; }
.yangyu { grid-area: 养鱼; }
.xigua { grid-area: 西瓜; }
<div class="container">
    <div class="putao"></div>
    <div class="longxia"></div>
    <div class="yangyu"></div>
    <div class="xigua"></div>
</div>
```

### grid-template
grid-template-rows，grid-template-columns和grid-template-areas属性的缩写。

### grid-column-gap和grid-row-gap
用来定义网格中网格间隙的尺寸。可以理解成田地之间走路的田垄宽度。
推荐使用column-gap和row-gap属性，兼容性也不错

### grid-gap
推荐使用gap属性作为缩写，grid-gap已经很老了。
grid-gap属性是grid-column-gap和grid-row-gap属性的缩写
```css
.container {
    grid-gap: <grid-row-gap> <grid-column-gap>;
}
```

## repeat()
repeat() 函数表示轨道列表的重复片段，允许以更紧凑的形式写入大量显示重复模式的列或行。
repeat(4, 1fr)

只能作用在grid-template-columns和grid-template-rows这两个CSS属性上，由于目前Firefox浏览器只支持在grid-template-columns属性上使用repeat()函数

Grid布局提升并不是repeat()函数，而是repeat()函数里面支持的那些关键字和函数，以及整个全新的CSS体系

### auto-fill
根据Grid布局中每一个子项的尺寸自动计算需要填充的数量
计算规则是，当前列表数量下的总尺寸不会超出Grid容器的最大正整数值。

### auto-fit
会把空的匿名格子进行折叠合并
如果Grid容器的尺寸特别的宽，则最后会有一些空的格子会合并成1个，且宽度是0

## gap属性
grid布局，Multi-column布局，以及Flex布局的间隙现在也都统一使用gap属性了。
{% asset_img gap.png %}

## minmax()
定义了一个长宽范围的闭区间，它与CSS 网格布局一起使用。
```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
}
```
[demo](https://codepen.io/xboxyan/pen/zYYgYdL)