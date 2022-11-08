---
title: vue3
date: 2022-02-12 16:42:22
categories:
- Frame
tags:
- vue3
---

# Base
技术选型
vue生态 + 工程化的最佳实践

阅读源码

vue3 + TypeScript + pinia(Vuex5) + vue-router

工程化：（循序渐进）
Vite + pnpm + eslint + 各种规范（自动化测试）

复杂度够高的一个项目，不是页面多

Composition 组合 API、基于 Proxy 的响应式系统、自定义渲染器

一个项目 增删改查 实现功能
1. 数据量大（过万条数据），复杂（5层以上）的场景
2. 完成增删改查后，研发效率的提升（组件库，自动化发布部署CI/CD，写了小工具plugin，团队项目规范）
3. 性能（跑的更快，首屏渲染提高，交互更流畅）
4. 用户体验
5. 项目质量和稳定性

技术选型
1. 框架vue3
2. 语言 Typescript
3. 包管理 pnpm
4. 路由 vue-router
5. 数据管理 pinia
6. vue的工具库 vueuse
7. 组件库：（自己封装一些组件）element3 elementplus naiveui antd-vue
8. 构建工具 vite
9. css预编译器 sass
10. 网络请求：axios（使用ts的类型限制）
11. 代码规范：eslint prettier（尽可能的松散）
12. git的规范 分支管理，hook来做eslint或者单测
13. 代码的部署 github action（纯前端的部署）
14. 自动化测试 vitest // 封装组件时才用
15. 工具函数 lodash
16. 日期处理 dayjs

## 构建项目
pnpm：没有最快只有更快

npm install -g pnpm

pnpm create vite

安装依赖包
pnpm i
Progress: resolved 111, reused 111, downloaded 0, added 111, done
reused 复用的模块

### 项目初始化
删除app.vue里面的内容
安装 vue 提示插件：volar

### Options API 改为 Composition API
``` ts
import { ref } from "vue";
export default{
  setup(){
    let count = ref(2)
    function add(){
      count.value++
    }
    return {count,add}
  }
}

// 简写
<script lang="ts" setup>
import { ref } from "vue";
let val = ref('')
// ref定义的，取值都要.value
console.log(val.value)
```

### ts类型
```ts
<script lang="ts" setup>
import { ref } from "vue";
// 第一种方式:范型  推荐使用
let val = ref<string>('')

// 第二种方式
import { ref, Ref } from "vue";
let val:Ref = ref('')
```

## 入门
### todomvc
基本的增删改查，所有的框架都建议先写一个todo mvc
```ts
// computed 读和写不同的操作
let allDone = computed<boolean>({
  get(){
    return active.value === todos.value.length
  },
  set(value:boolean){
    todos.value.forEach(todo => todo.done = value)
  }
})
```

# DOC
## api
### Options
``` vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

### Composition
导入API函数
组合式API Composition 与 `<script setup></script>` 配合使用；setup 属性，是一个标识。
与cocos组件类似

优点：
1. 逻辑复用
2. 自由灵活
3. 类型推导
4. 生产包小

但：
需要对 Vue 的响应式系统有更深的理解才能高效使用
``` vue
<script setup>
import { ref, onMounted } from 'vue'
const count = ref(0)

function increment() {
  count.value++
}

// 生命周期钩子
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

### 计算属性
推荐用`计算属性`来描述依赖响应式状态的复杂逻辑
```vue
<!-- 之前 -->
<span>{{ books.length > 0 ? 'Yes' : 'No' }}</span>
<!-- 现在 -->
<span>{{show}}</span>
<script lang="ts">
  const show = computed(()=>{
    return books.length > 0 'Yes': 'No'
  })
</script>
```

注意：
计算属性的 getter 应只做计算而没有任何其他的副作用，这一点非常重要，请务必牢记。举例来说，不要在 getter 中做异步请求或者更改 DOM！

### 类与样式绑定
```vue
<!-- 方式一 -->
<div
  class="static"
  :class="{ active: isActive, 'text-danger': hasError }"
></div>

<!-- 方式二 -->
<div :class="classObject"></div>
<script>
  const classObject = reactive({
    active: true,
    'text-danger': false
  })
</script>

<!-- 方式三 -->
<div :class="[activeClass, errorClass]"></div>
<script>
const activeClass = ref('active')
const errorClass = ref('text-danger')
</script>
```

#### 绑定内联样式
```vue
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

### 列表渲染
展示过滤或排序后的结果
```vue
<li v-for="n in evenNumbers">{{ n }}</li>
<script>
  const numbers = ref([1, 2, 3, 4, 5])
  const evenNumbers = computed(() => {
    return numbers.value.filter((n) => n % 2 === 0)
  })
</script>
```
