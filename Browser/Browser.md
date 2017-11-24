# 浏览器结构组成
浏览器一般由七个模块组成:
* `User Interface（用户界面）` －包括地址栏、后退/前进按钮、书签目录等，也就是你所看到的除了页面显示窗口之外的其他部分
* `Browser engine（浏览器引擎）` －可以在用户界面和渲染引擎之间传送指令或在客户端本地缓存中读写数据等，是浏览器中各个部分之间相互通信的核心
* `Rendering engine（渲染引擎）` －解析DOM文档和CSS规则并将内容排版到浏览器中显示有样式的界面，也有人称之为排版引擎，我们常说的浏览器内核主要指的就是渲染引擎
* `Networking（网络）` －用来完成网络调用或资源下载的模块
* `JavaScript Interpreter（js解释器）` －用来解释执行JS脚本的模块，如 V8 引擎、JavaScriptCore
* `UI Backend（UI 后端）` -用来绘制基本的浏览器窗口内控件，如输入框、按钮、单选按钮等，根据浏览器不同绘制的视觉效果也不同，但功能都是一样的
* `Date Persistence（数据持久化存储）` －浏览器在硬盘中保存 cookie、localStorage等各种数据，可通过浏览器引擎提供的API进行调用  

![](https://user-gold-cdn.xitu.io/2017/11/1/81abbf6319b1ad27dd3914ad39c04cd4?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)  

作为前端开发人员，我们需要重点理解`渲染引擎`的工作原理，灵活应用`数据存储技术`，在实际项目开发中会经常涉及到这两个部分，尤其是在做项目性能优化时，理解浏览器渲染引擎的工作原理尤为重要。而其他部分则是由浏览器自行管理的，开发者能控制的地方较少。