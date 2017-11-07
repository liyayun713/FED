# web调试-chrome开发者工具指南
### 1、Elements
* 选择元素
* 移动端适配
* Online模拟网络
* 切换横竖屏
* ##取色器##
* 元素状态筛选
* html布局调试
* css3动画曲线调试（贝塞尔曲线）
![](https://github.com/liyayun713/FED/blob/master/images/css3-bezier.png)

### 2、Console
* console.log
* console.info
* console.warn
* console.error
* console.time和console.timeEnd
```js
console.time();
for(let i=0;i<10000;i++){
    
}
console.timeEnd();
```
* console.table
```js
let arr=[
	{a:1,b:2,c:3},
	{a:1,b:4,c:3},
	{a:3,b:2,c:3},
	{a:4,b:2,c:3},
	{a:1,b:5,c:3},
	{a:1,b:9,c:3},
	{a:1,b:2,c:7}
];
console.table(arr)
```
* $:返回第一个符合条件的元素，相当于document.querySelector
* $$:返回所有符合条件的元素，相当于document.querySelectorAll
* getEventListeners作用就是查找并获取选定元素的事件

### 3、Network
### 4、Sources
* breakpoint
* debugger;
* 查找和切换文件
* 整理代码 {}

### 5、Performance(Timeline)
###### 性能优化的时候使用
### 6、Application
* cookie
* localStorage和sessionStorage
* 缓存(Cache)
* indexedDB
* Frames 将页面上的资源按frame类别进行组织显示。顶级的top是一个主文档，在top下面是主文档的Fonts、Images、Scripts、Stylesheets等资源。最后一个就是主文件自身
