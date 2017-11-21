# Vue的各种监听
### watch属性：watch是vue实列的一个属性，它是一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性
### watch的几种方法
```js
var vm = new Vue({
  data: {
    a: 1,
    b: 2,
    c: 3
  },
  methods: {
    someMethod () {
      // ...
    },
  },
  watch: {
    //第一种写法 适用于普通变量（简单类型的值的观测写法）
    a: function (val, oldVal) {
      console.log('new: %s, old: %s', val, oldVal)
    },
    
    // 第二种写法：方法名
    b: 'someMethod',
    
    // 第三种写法：深度 watcher(能观测对象c下多重属性变化)（复杂类型的值的观测写法）
    c: {
      //当c变化后会回调handler函数
      handler: function (val, oldVal) { /* ... */ },
      deep: true
    }
  }
})
vm.a = 2 // -> new: 2, old: 1
```
### 注意:不能使用箭头函数定义watcher（回调）函数，因为箭头函数绑定了父级作用域的上下文，所以里面的 this 将不会按照期望指向 Vue 实例
