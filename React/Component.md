# 组件
### 接下来我们封装一个输出 "Hello World！" 的组件，组件名为 HelloMessage
```jsx
var HelloMessage = React.createClass({
  render: function () {
    return {
      <div>Hello World!</div>;
    }
  }
})

ReactDOM.render(
  <HelloMessage />,
  document.getElementById('id')
)
```

#### 实例解析：
**React.createClass 方法用于生成一个组件类 HelloMessage。  

**<HelloMessage /> 实例组件类并输出信息。  

### 如果我们需要向组件传递参数，可以使用 this.props 对象,实例如下：
```jsx
var HelloMessage = React.createClass({
  render: function() {
    return <div>Hello, {this.props.name}</div>;
  }
})

ReactDOM.render(
  <HelloMessage name="world!">,
  document.getElementById('id')
)
```
### 复合组件
我们可以通过创建多个组件来合成一个组件，即把组件的不同功能点进行分离。  

以下实例我们实现了输出网站名字和网址的组件：  

```jsx
<body>
    <div id="example"></div>
    <script type="text/babel">
       var WebSite = React.createClass({
          render: function() {
            return (
              <div>
                <Name name={this.props.name} />
                <Link site={this.props.site} />
              </div>
            );
          }
        });

        var Name = React.createClass({
          render: function() {
            return (
              <h1>{this.props.name}</h1>
            );
          }
        });

        var Link = React.createClass({
          render: function() {
            return (
              <a href={this.props.site}>
                {this.props.site}
              </a>
            );
          }
        });

        ReactDOM.render(
          <WebSite name="菜鸟教程" site=" http://www.runoob.com" />,
          document.getElementById('example')
        );
    </script>
  </body>
```
