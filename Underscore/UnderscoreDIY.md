# 如何实现自己的Underscore
```js
(function(){
    var root = this;    // 严格模式下会报错

    var _ = {};

    root._ = _;

    // 添加方法
    _.reverse = function(string){
        return string.split('').reverse().join('');
    }

})()

// 使用
_.reverse('Tony Li');
=> 'iL ynoT'
```
#### 我们将所有的方法添加到一个名为 _ 的对象上，然后将该对象挂载到全局对象上。之所以不直接 window._ = _ 是因为我们写的是一个工具函数库，不仅要求可以运行在浏览器端，还可以运行在诸如 Node 等环境中。
