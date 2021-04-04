---
title: vuex的getter
date: 2021-04-04 12:27:13
tags:
- vuex 
- vue学习
categories: Vue
---
## vuex 的 getters
正常来说，`state` 中的值是可以在组件中通过 `computed` 进行计算求值的  
但是如果十个，几十个页面都需要使用同一个计算属性  
这时候我们是不可能在每个页面都写一次同样的计算属性的。  
因此，`vuex` 中有了 `getter` ，可以理解为是 `store` 的计算属性  
> 就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。
`getter` 接受 `state` 作为第一个参数
```javascript
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    },
    
    doneTodosCount: (state, getters) => {
      return getters.doneTodos.length
    }
  }
})
```
页面中使用 `getter` 的方法和 `state` 类似，通过`this.$store.getter.doneTodos`来获得计算后的state的值

`getter` 可以接收 `getters` 作为第二个参数，之前定义的 `getter` 属性可以直接参与计算
```javascript
 getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    },
    
    doneTodosCount: (state, getters) => {
      return getters.doneTodos.length
    }
  }
```
使用闭包传递自定义参数  
简单说就是返回值是一个函数，在使用的时候记得将参数传进去并进行调用  
可以实现传递我们自定义参数的需求
```javascript
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
    // 使用  获取 id 值为 116 的数据
    getTodoById(116)

```
`getter` 也支持辅助函数 `mapGetters` 具体写法有对象语法和数组语法 ,同样可以将返回的 getter 混入到外部计算属性

```JavaScript
// 字符串对应的就是 getters 里的方法名
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}

// 传递对象作为参数可以在传递的时候起别名
...mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```
> 总结一下就是 getters 和 state 的用法基本一致 ，用起来也超级简单