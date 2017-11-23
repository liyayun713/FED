# JavaScript函数柯里化
## 什么是柯里化
### 官方说法
是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术
### 方便理解
如果我们需要实现一个求三个数之和的函数：
```js
function add(x, y, z) {
  return x + y + z;
}
console.log(add(1, 2, 3)); // 6
```
```js
var add = function(x) {
  return function(y) {
    return function(z) {
      return x + y + z;
    }
  }
}

var addOne = add(1);
var addOneAndTwo = addOne(2);
var addOneAndTwoAndThree = addOneAndTwo(3);

console.log(addOneAndTwoAndThree);
```
用ES6的箭头函数，我们可以将上面的add实现成这样：
```js
const add = x => y => z => x + y + z;
```
