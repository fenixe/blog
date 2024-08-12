---
title: Utils
date: 2020-06-18 16:44:09
categories:
- Coding
tags:
- Coding
- Tool
---

# Base

# ULID
当在同一毫秒内生成 ULID 时，我们可以提供一些有关排序顺序的保证。也就是说，如果检测到同一毫秒，则组件random在最低有效位位置增加 1 位（带进位）。例如：
``` js
import { monotonicFactory } from 'ulid'

const ulid = monotonicFactory()

// Assume that these calls occur within the same millisecond
ulid() // 01BX5ZZKBKACTAV9WEVGEMMVRZ
ulid() // 01BX5ZZKBKACTAV9WEVGEMMVS0
```

如果在极不可能的情况下，您在同一毫秒内成功生成超过 2^80 个ULID，或者导致随机组件溢出，则生成将失败。
``` js
import { monotonicFactory } from 'ulid'

const ulid = monotonicFactory()

// Assume that these calls occur within the same millisecond
ulid() // 01BX5ZZKBKACTAV9WEVGEMMVRY
ulid() // 01BX5ZZKBKACTAV9WEVGEMMVRZ
ulid() // 01BX5ZZKBKACTAV9WEVGEMMVS0
ulid() // 01BX5ZZKBKACTAV9WEVGEMMVS1
...
ulid() // 01BX5ZZKBKZZZZZZZZZZZZZZZX
ulid() // 01BX5ZZKBKZZZZZZZZZZZZZZZY
ulid() // 01BX5ZZKBKZZZZZZZZZZZZZZZZ
ulid() // throw new Error()!
```

## 业务量分析
2020年淘宝“双十一”订单峰值：每秒583,000个订单。
每毫秒：583个。

ULID每毫秒最大数量：2^80 = 1,208,925,800,000,000,000,000,000
