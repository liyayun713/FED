# Vue单向数据流
Prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是反过来不会。这是为了防止子组件无意间修改了父组件的状态，来避免应用的数据流变得难以理解。<br/>
## 如果想修改props中传入的数据，正确的做法为
* 定义一个局部变量，并用prop的值去初始化它
```javascript
props: {
  papData: String
},
data () {
  return {
    childData: this.papData
  };
}
```
* 使用计算属性
```js
props: {
  papData: String
},
computed: {
  childData () {
    return this.papData.trim().toLowerCase();
  }
}
```
