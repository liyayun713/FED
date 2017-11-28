# Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式
把组件的共享状态抽取出来，以一个**全局单例模式**管理，在这种模式下，我们的组件树构成了一个巨大的“视图”，不管在树的哪个位置，任何组件都能获取状态或者触发行为

![](https://vuex.vuejs.org/zh-cn/images/vuex.png)
  
## 什么情况下我应该使用 Vuex？
如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。确实是如此——如果您的应用够简单，您最好不要使用 Vuex。一个简单的 global event bus 就足够您所需了。但是，如果您需要构建是一个中大型单页应用，您很可能会考虑如何更好地在组件外部管理状态，Vuex 将会成为自然而然的选择。

## 开始
```js
import Vuex from 'vuex';
Vue.use(Vuex);

const store = new Vuex({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++;
    }
  }
});
```
执行
```js
store.commit('increment');
console.log(store.state.count);   // 1
```

## 核心概念
### 1、state -- 单一状态树
Vuex 使用**单一状态树**，用一个对象就包含了全部的应用层级状态。至此它便作为一个**“唯一数据源 (SSOT)”**而存在。这也意味着，每个应用将仅仅包含一个 store 实例。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。  

#### 在Vue组件中获得Vuex状态

```js
// 创建一个组件
const Counter = {
  template: '<div>{{count}}</div>',
  computed: {
    count () {
      return store.state.count
    }
  }
};
```

每当 store.state.count 变化的时候, 都会重新求取计算属性，并且触发更新相关联的 DOM。  

然而，这种模式导致组件依赖全局状态单例。在模块化的构建系统中，在每个需要使用 state 的组件中需要频繁地导入，并且在测试组件时需要模拟状态。  

Vuex 通过 store 选项，提供了一种机制将状态从根组件“注入”到每一个子组件中（需调用 Vue.use(Vuex)）：
```js
const app = new Vue({
  el: '#app',
  // 把 store 对象提供给 “store” 选项，这可以把 store 的实例注入所有的子组件
  store,
  components: { Counter },
  template: `
    <div class="app">
      <counter></counter>
    </div>
  `
})
```
通过在根实例中注册 store 选项，该 store 实例会注入到根组件下的所有子组件中，且子组件能通过 this.$store 访问到。让我们更新下 Counter 的实现：  

```js
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return this.$store.state.count
    }
  }
}
```

### 2、Getter -- 可以认为是 store 的计算属性
### 3、Mutations -- 更改 Vuex 的 store 中的状态的唯一方法是提交 mutation
Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数：  
```js
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
### 4、Action -- 类似于 mutation
### 5、Module -- 模块化
由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。  

为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：  
```js
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```

## 项目结构
Vuex 并不限制你的代码结构。但是，它规定了一些需要遵守的规则：  

* 应用层级的状态应该集中到单个 store 对象中

* 提交 mutation 是更改状态的唯一方法，并且这个过程是同步的

* 异步逻辑都应该封装到 action 里面

