# 扩展运算符
扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将`一个数组`转为`用逗号分隔的参数序列`。

```js
console.log(...[1, 2, 3]);
// 1 2 3

console.log(1, ...[2, 3, 4], 5);
// 1 2 3 4 5

console.log(...document.querySelectorAll('div'));
// [<div>, <div>, <div>]
```

### 该运算符主要用于函数调用。

```js
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers) // 42
```

* 上面代码中，array.push(...items)和add(...numbers)这两行，都是函数的调用，它们的都使用了扩展运算符。
* `该运算符将一个数组，变为参数序列`。
* 扩展运算符与正常的函数参数可以结合使用，非常灵活。
