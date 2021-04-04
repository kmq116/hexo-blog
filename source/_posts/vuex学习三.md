---
title: vuex的mutation
date: 2021-04-04 13:00:07
tags:
- vuex 
- vue学习
categories: Vue
---
之前的文章提到了，state 的状态可以直接参与计算或者通过 getter 进行计算  
如果要改变 store 的值，则需要通过 mutation 来进行操作  
> 每个 mutation 都有一个字符串的 **事件类型 (type)** 和 一个 **回调函数 (handler)** 。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 `state` 作为第一个参数
```javascript
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
```
如果要使用这个函数，是不能直接调用的，正确的使用方式是通过访问 store 实例 `this.$store.commit("increment")` 来进行调用

在 commit 的时候可以向 mutation 传递参数，参数类型可以任意，这里以对象为例子

```JAVASCRIPT
// ...
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}

// 调用
store.commit('increment', {
  amount: 10
})

// 另一种提交风格
store.commit({
  type: 'increment',
  amount: 10
})
```

### Vuex的响应式规则
- 在 store 中初始化好所有的属性
- 如果在对象上添加新的属性 使用 `Vue.set()` 或者对象展开语法 `...` 的方式，用新对象替换老对象
