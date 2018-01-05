# 函数节流

函数柯里化
```js
function debounce (fn, delay) {
  if (timer) return;
  var timer;
  timer = setTimeout(() => {
    fn
  }, delay);
}
```
