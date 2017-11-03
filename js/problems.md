# 一些有趣的js题目
### 知识点：词法分析期、执行期；变量提升
```js
b();              // 'i am b'
console.log(a);   // undefined

var a = 'i am a';

function b () {
  console.log('i am b');
}
```
### 知识点：因为 b 是在全局环境中声明的，所以 value 的声明会在全局环境下寻找
```js
function b() {
  console.log(value);
}
function a() {
  var value = 2;
  b();
}

var value = 1;
a();    // 1
```
