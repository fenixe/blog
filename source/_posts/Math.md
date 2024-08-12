---
layout: other
title: Math数学
date: 2020-03-23 09:33:26
categories:
- Math数学
tags:
- Math数学
---

# Base
## 科学计数法
科学计数法是一种简洁表示非常大或非常小的数的方法。

结构：a×10^b
- a 是一个小数，通常在1到10之间（包括1，但不包括10）。
- b 是一个整数，表示10的幂次。

### 例子
ULID中：If, in the extremely unlikely event that, you manage to generate more than 2^80 ULIDs within the same millisecond, or cause the random component to overflow with less, the generation will fail.

2^80 = 1.2089258e+24
- 1.2089258：这是系数部分，表示一个小数。
- e：表示“乘以10的幂次”。这是科学计数法中的标准符号。
- +24：表示10的幂次是正24。

所以：1.2089258e+24 表示的数是 1,208,925,800,000,000,000,000,000，即一个非常大的数。