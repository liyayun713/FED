# this call apply bind
### this 永远指向最后调用它的那个对象
```js
var name = "windowsName";
var a = {
    name: "Li",
    fn : function () {
        console.log(this.name);
    }
}

var f = a.fn;
f();    // windowsName
```
```js
var name = "windowsName";
function fn() {
    var name = 'fnName';
    innerFunction();    // 相当于this.innerFunction()，this指向window
    function innerFunction() {
        console.log(this.name);
    }
}
fn();   // windowsName
```
### 怎么改变this的指向
* arrow function
* call apply bind
* new 实例化一个对象
* 使用 self=this
```js
// 使用箭头函数
var name = "windowsName";
var a = {
    name : "Cherry",
    func1: function () {
        console.log(this.name)     
    },
    func2: function () {
        setTimeout( () => {
            this.func1()
        },100);
    }
};
a.func2()     // Cherry
```
```js
// 使用 self = this;
func2: function () {
    var _this = this;
    setTimeout( function() {
        _this.func1()
    },100);
}
```
```js
// 使用apply、call、bind
var a = {
    name : "Cherry",
    func1: function () {
        console.log(this.name)
    },
    func2: function () {
        setTimeout(  function () {
            this.func1()
        }.bind(a)(),100);       // 本例中apply、call、bind相同用法
    }
};
a.func2();      // 'Cherry'
```
## apply、call、bind区别
