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
