---
title: guide
date: 2020-05-27 20:30:33
categories:
- guide
tags:
- guide
---

编码规范 
[google](https://developers.google.com/style/html-formatting)
[google](https://google.github.io/styleguide/htmlcssguide.html)

# HTML
## 缩进
次缩进2个空格，不要使用 tab 或者混合 tab 和空格的缩进。

对元素和属性使用全小写。

不要在行尾留下尾随空格。

# API
在API请求参数的命名约定上，并没有一个绝对的标准，更多的取决于您或者团队遵循的风格指南或者已有的API设计。
通常情况下，有两种主流的命名方式：
1、Camel Case (questionNo): 在这种命名约定中，除了第一个单词外，其他单词的首字母大写。这是Java和JavaScript等编程语言中常用的风格。
2、Snake Case (question_no): 此命名约定使用下划线_来分隔单词。这种风格经常用在Python编程中，也在诸如Ruby on Rails的框架中比较普遍。此外，在制定JSON API规范时，有时候也会使用snake case。
更合理的选择取决于您的使用场景：
· 如果您的API主要是供Java、C#或JavaScript的客户端使用，那么可能倾向于使用Camel Case风格来保持一致性。
· 如果API的消费者是Python或Ruby客户端，或者您的团队已有API遵循了Snake Case命名，那么使用Snake Case可能会更合理。
· 对于RESTful API来说，有些开发者更偏好使用Snake Case，因为URL和查询参数通常不区分大小写，且在某些情况下Snake Case可以提高可读性。
无论选择哪一种，最重要的是保持一致性。确保整个API的参数命名方式都是统一的。如果您加入了一个已经开始的项目，请遵循该项目已经设定的规范。在团队协作中，可能需要根据团队内部或项目的API设计指南来决定。
