# ES6常用语法
### 1、let & const
let和var区别在于，let有块级作用域的的区分概念，const初始化赋值之后就不能再改变赋值
### 2、arrow function
当使用了setTimeout或者setInterval的时候，es5下this为window<br/>
箭头函数没有this，它的this是继承外面的，因此内部的this就是外层代码块的this
### 3、template string 模板字符串
```js
return `剩余时间${d}天${h}小时${m}分钟${s}秒"`;
```
插入html元素
```js
et obj={
    author:'守候',
    time:'2017.11.8',
    thing:'看下模板字符串的方便性。'
}
$("#test").append(
  `<p>
      这是<i>${obj.author}</i>
      写的一个实例。这个实例是为了
      <i> ${obj.thing}</i>
      <span>写作日期是：${obj.time}</span>
   </p>`
); 
```
### 4、destructuring 解构赋值
```js
let info={name: "守候", sex: "男"};
let {name,sex}=info;
console.log(name,sex);    // "守候" "男"
```
### 5、default & rest
### 6、import & export
