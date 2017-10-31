# Vue组件间通信
### 一、父子组件通信
###	   1、props
```html
<template>
  <div>
    <child :num="num"></child>
  </div>
</template>

<script>
   // 父组件中通过':'绑定属性，子组件通过'props'接收
   // 子组件通过this.$emit('emitMsg', msg)发射，父组件通过@emitMsg="cb"监听属性，触发回调函数
</script>
``` 
###	    2、使用$parent、$children
###	二、非父子组件通信---global_bus
###	三、复杂应用---Vuex
