---
title: vuex的state
date: 2021-04-04 11:11:30
tags:
- vuex 
- vue学习
categories: Vue
---
## 为什么使用 vuex
先来看这样一张图

![Alt text](../images/vuex/flow.png)
视图，事件，数据，三者按照图的方式互相影响的  
但是如果多个组件，多个页面需要引用同一个值的时候，或者多个页面的行为要改变某个值时，再使用组件传值的方式就会异常麻烦，这时候可以用到vuex
> 据vuex官方指导，如果不打算开发大型单页面应用，使用vuex时冗余的，如果应用足够简单，最好不要使用vuex。
### 里面都有什么 
* 通过`new`的方式可以创建一个`store`实例
实例内容如下
```javascript
import Vuex from "vuex";

const store = new Vuex.Store({
  state: {},
  mutations: {}, 
  actions:{},
  getters:{},
  modules:{}
})
```
> `state`: 存储在 Vuex 中的数据和 Vue 实例中的 data 遵循相同的规则  

组件可以通过 `this.$store` 来访问到 `store` 实例  
如要访问`state`中的`counter`属性，可以像下面这种方式
```javascript
<template>
  <div>
    <h2>Vuex组件</h2>
    <div>{{ $store.state.counter }}</div>
  </div>
</template>
```
上面写法是取单个状态的写法，如果去获取多个状态可以使用 `mapState` 函数

```javascript
<template>
  <div>
    <h2>Vuex组件</h2>
    <div>{{ $store.state.counter }}</div>
    <div>辅助函数的counter{{ counter }}</div>
    <div>带组件内参数的{{ localState }}</div>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  data() {
    return {
      number: 1,
    };
  },
  computed: mapState({
    // 箭头函数写法
    // counter: (state) => state.counter,

    //传递一个字符串写法
    // counter: "counter",

    // 想继续使用 this 获取组件内属性进行计算的写法
    localState(state) {
      return state.counter + this.number;
    },
  }),
};
</script>

```
因为 `mapState` 返回的是一个对象，所以最优雅的写法是使用对象展开语法 `...` 将返回的对象混入到外部对象中，代码如下：
```javascript
  computed: {
    localState() {
      return this.counter + this.number;
    },
    
    ...mapState({
      // 箭头函数写法
      counter: (state) => state.counter,
      //传递一个字符串写法
      // counter: "counter",
    }),
  },
```
>使用vuex的时候不代表所有的数据都要放入到vuex中，这样做的坏处是代码会变得冗长和不直观，具体如何使用请根据开发需要进行权衡和确定。

