# JSX
React 使用 JSX 来替代常规的 JavaScript。  

JSX 是一个看起来很像 **XML** 的 JavaScript 语法扩展。  

```jsx
ReactDOM.render(
  <div>hello，world</div>,
  document.getElementById('example')
)
```

我们不需要一定使用 JSX，但它有以下优点：

* JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
* 它是类型安全的，在编译过程中就能发现错误。
* 使用 JSX 编写模板更加简单快速。  

### 我们可以在以上代码中嵌套多个 HTML 标签，需要使用一个 div 元素包裹它，实例中的 p 元素添加了自定义属性 data-myattribute，添加自定义属性需要使用 data- 前缀。

```jsx
 ReactDOM.render(
    <div>
     <h1>菜鸟教程</h1>
     <h2>欢迎学习 React</h2>
     <p data-myattribute = "somevalue">这是一个很不错的 JavaScript 库!</p>
    </div>,
    document.getElementById('example')
 )
```  

### 独立文件
你的 React JSX 代码可以放在一个独立文件上，例如我们创建一个 helloworld_react.js 文件，代码如下：
```jsx
 ReactDOM.render(
   <h1>Hello, world!</h1>,
   document.getElementById('example')
 );
```  

然后在 HTML 文件中引入该 JS 文件：
```jsx
<body>
 <div id="example"></div>
 <script type="text/babel" src="helloworld_react.js"></script>
</body>
```  

### Javascript 表达式
我们可以在 JSX 中使用 JavaScript 表达式。表达式写在花括号 {} 中。实例如下：  

```jsx
ReactDOM.render(
  <div>
    <h1>{1+1}</h1>
  </div>,
  document.getElementById('example')
);
```  

在 JSX 中不能使用 if else 语句，但可以使用 conditional (三元运算) 表达式来替代。以下实例中如果变量 i 等于 1 浏览器将输出 true, 如果修改 i 的值，则会输出 false.  

```jsx
ReactDOM.render(
  <div>
    <h1>{i == 1 ? 'True!' : 'False'}</h1>
  </div>,
  document.getElementById('example')
);
```

### 样式
React 推荐使用内联样式。我们可以使用 camelCase 语法来设置内联样式. React 会在指定元素数字后自动添加 px 。以下实例演示了为 h1 元素添加 myStyle 内联样式：  

```jsx
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
ReactDOM.render(
    <h1 style = {myStyle}>菜鸟教程</h1>,
    document.getElementById('example')
);
```  

### 注释
1. 在标签内部的注释需要花括号

2. 在标签外的的注释不能使用花括号 

```jsx
ReactDOM.render(
    <div>
    <h1>菜鸟教程</h1>
    {/*注释...*/}
     </div>,
    document.getElementById('example')
);
```

### 数组
JSX 允许在模板中插入数组，数组会自动展开所有成员：  

```jsx
var arr = [
  <h1>菜鸟教程</h1>,
  <h2>学的不仅是技术，更是梦想！</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
```

### HTML 标签 vs. React 组件
React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)。  

要渲染 HTML 标签，只需在 JSX 里使用小写字母的标签名。  

```jsx
var myDivElement = <div className="foo" />;
ReactDOM.render(myDivElement, document.getElementById('example'));
```  

要渲染 React 组件，只需创建一个大写字母开头的本地变量。  

```jsx
var MyComponent = React.createClass({/*...*/});
var myElement = <MyComponent someProperty={true} />;
ReactDOM.render(myElement, document.getElementById('example'));
```

React 的 JSX 使用大、小写的约定来区分本地组件的类和 HTML 标签。

#### 注意: 由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。
