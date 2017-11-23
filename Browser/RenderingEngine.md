# 浏览器渲染引擎（RenderingEngine）
#### 浏览器渲染引擎是由各大浏览器厂商依照 W3C 标准自行研发的，也被称之为`「浏览器内核」`
#### 目前，市面上使用的主流浏览器内核有5类：Trident、Gecko、Presto、Webkit、Blink。
* **Trident：** 俗称 IE 内核，也被叫做 MSHTML 引擎，目前在使用的浏览器有 IE11 -，以及各种国产多核浏览器中的IE兼容模块。另外微软的 Edge 浏览器不再使用 MSHTML 引擎，而是使用类全新的引擎 EdgeHTML
* **Gecko：** 俗称 Firefox 内核，Netscape6 开始采用的内核，后来的 Mozilla FireFox（火狐浏览器）也采用了该内核，Gecko 的特点是代码完全公开，因此，其可开发程度很高，全世界的程序员都可以为其编写代码，增加功能。因为这是个开源内核，因此受到许多人的青睐，Gecko 内核的浏览器也很多，这也是 Gecko 内核虽然年轻但市场占有率能够迅速提高的重要原因
* **Presto：** Opera 前内核，为啥说是前内核呢？因为 Opera12.17 以后便拥抱了 Google Chrome 的 Blink 内核，此内核就没了寄托
* **Webkit：** Safari 内核，也是 Chrome 内核原型，主要是 Safari 浏览器在使用的内核，也是特性上表现较好的浏览器内核。也被大量使用在移动端浏览器上
* **Blink：**  由 Google 和 Opera Software 开发，在Chrome（28及往后版本）、Opera（15及往后版本）和Yandex浏览器中使用。Blink 其实是  **Webkit** 的一个分支，添加了一些优化的新特性，例如跨进程的 iframe，将 DOM 移入 JavaScript 中来提高 JavaScript 对 DOM 的访问速度等，目前较多的移动端应用内嵌的浏览器内核也渐渐开始采用 Blink
## 渲染引擎的工作流程
浏览器渲染引擎最重要的工作就是将 HTML 和 CSS 文档解析组合最终渲染到浏览器窗口上。如下图所示，渲染引擎在接受到 HTML 文件后主要进行了以下操作：解析 HTML 构建 DOM 树 -> 构建渲染树 -> 渲染树布局 -> 渲染树绘制
![](https://user-gold-cdn.xitu.io/2017/11/1/6555b409fcdee45a07b5362d93e879ff?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
