# 安装
## 一、script 标签引用
```html
<script src="https://cdn.bootcss.com/react/15.4.2/react.min.js"></script>
<script src="https://cdn.bootcss.com/react/15.4.2/react-dom.min.js"></script>
<script src="https://cdn.bootcss.com/babel-standalone/6.22.1/babel.min.js"></script>
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <script src="https://cdn.bootcss.com/react/15.4.2/react.min.js"></script>
    <script src="https://cdn.bootcss.com/react/15.4.2/react-dom.min.js"></script>
    <script src="https://cdn.bootcss.com/babel-standalone/6.22.1/babel.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
  </body>
</html>
```

* react.min.js - React 的核心库
* react-dom.min.js - 提供与 DOM 相关的功能
* babel.min.js - Babel 可以将 ES6 代码转为 ES5 代码，这样我们就能在目前不支持 ES6 浏览器上执行 React 代码。Babel 内嵌了对 JSX 的支持。通过将 Babel 和 babel-sublime 包（package）一同使用可以让源码的语法渲染上升到一个全新的水平。

#### 如果我们需要使用 JSX，则 <script> 标签的 type 属性需要设置为 text/babel。
## 二、npm 安装
### cnpm 安装
国内使用 npm 速度很慢，你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:  
  
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
npm config set registry https://registry.npm.taobao.org
npm config get registry
```

### 使用 create-react-app 快速构建 React 开发环境
create-react-app 是来自于 Facebook，通过该命令我们无需配置就能快速构建 React 开发环境  
**create-react-app 自动创建的项目是基于 Webpack + ES6**  

执行以下命令创建项目：  
```
$ cnpm install -g create-react-app
$ create-react-app my-app
$ cd my-app/
$ npm start
```
