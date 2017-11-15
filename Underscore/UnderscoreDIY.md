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
