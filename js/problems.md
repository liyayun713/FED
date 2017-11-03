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
