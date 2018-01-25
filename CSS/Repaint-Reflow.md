# reflow回流（也叫重排）& repaint重绘
## 浏览器渲染机制
在讨论页面重绘、回流之前。需要对页面的呈现流程有些了解，页面是怎么把html结合css等显示到浏览器上的，下面的流程图显示了浏览器对页面的呈现的处理流程。可能不同的浏览器略微会有些不同。但基本上都是类似的。

![](https://upload-images.jianshu.io/upload_images/3029162-18abc70b3e6940d7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

1. 浏览器把获取到的HTML代码解析成1个 `DOM树`，HTML中的每个tag都是DOM树中的1个节点，根节点就是我们常用的document对象。DOM树里包含了所有HTML标签，包括display:none隐藏，还有用JS动态添加的元素等。

2. 浏览器把所有样式(用户定义的CSS和用户代理)解析成 `样式结构体`，在解析的过程中会去掉浏览器不能识别的样式，比如IE会去掉-moz开头的样式，而FF会去掉_开头的样式。

3. DOM Tree 和样式结构体组合后构建 `render tree`, render tree类似于DOM tree，但区别很大，render tree**能识别样式**，render tree中每个NODE都有自己的style，而且 render tree不包含隐藏的节点 (比如display:none的节点，还有head节点)，因为这些节点不会用于呈现，而且不会影响呈现的，所以就不会包含到 render tree中。注意 visibility:hidden隐藏的元素还是会包含到 render tree中的，因为visibility:hidden 会影响布局(layout)，会占有空间。根据CSS2的标准，render tree中的每个节点都称为`Box` (Box dimensions)，理解页面元素为一个具有填充、边距、边框和位置的盒子

4. 一旦render tree构建完毕后，浏览器就可以根据render tree来绘制页面了(GPU)

## 重排
当render tree中的**一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建**。这就称为回流(reflow)。每个页面至少需要一次回流，就是在页面第一次加载的时候。在回流的时候，浏览器会使渲染树中**受到影响的部分**失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘。

### 回流何时发生：
* 添加或者删除可见的DOM元素；

* 元素位置改变；

* 元素尺寸改变——边距、填充、边框、宽度和高度

* 内容改变——比如文本改变或者图片大小改变而引起的计算值宽度和高度改变；

* 页面渲染初始化；

* 浏览器窗口尺寸改变——resize事件发生时；

## 重绘
当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color。则就叫称为重绘。

### 注意：回流必将引起重绘，而重绘不一定会引起回流。

说到这里大家都知道回流比重绘的代价要更高，回流的花销跟render tree有多少节点需要重新构建有关系。

* 假设你直接操作body，比如在body最前面插入1个元素，会导致整个render tree回流，这样代价当然会比较高，
* 但如果是指body后面插入1个元素，则不会影响前面元素的回流。

## 聪明的浏览器
从上个实例代码中可以看到几行简单的JS代码就引起了6次左右的回流、重绘。而且我们也知道回流的花销也不小，如果每句JS操作都去回流重绘的话，浏览器可能就会受不了。所以很多浏览器都会优化这些操作，浏览器会维护1个队列，把所有会引起回流、重绘的操作放入这个队列，等队列中的操作到了一定的数量或者到了一定的时间间隔，浏览器就会flush队列，进行一个批处理。这样就会让多次的回流、重绘变成一次回流重绘。

虽然有了浏览器的优化，但有时候我们写的一些代码可能会强制浏览器提前flush队列，这样浏览器的优化可能就起不到作用了。当你请求向浏览器请求一些 style信息的时候，就会让浏览器flush队列，比如：

1. offsetTop, offsetLeft, offsetWidth, offsetHeight

2. scrollTop/Left/Width/Height

3. clientTop/Left/Width/Height

4. width,height

5. 请求了getComputedStyle(), 或者 IE的 currentStyle

当你请求上面的一些属性的时候，浏览器为了给你最精确的值，需要flush队列，因为队列中可能会有影响到这些值的操作。即使你获取元素的布局和样式信息跟最近发生或改变的布局信息无关，浏览器都会强行刷新渲染队列。

## 优化点
减少回流、重绘其实就是需要减少对render tree的操作（合并多次多DOM和样式的修改），并减少对一些style信息的请求，尽量利用好浏览器的优化策略。具体方法有：
1. 直接改变className，如果动态改变样式，则使用cssText（考虑没有优化的浏览器），不单独设置css属性，如
```js
document.body.style.width='100px';
```

2. 让要操作的元素进行”离线处理”，处理完后一起更新
* 使用DocumentFragment进行缓存操作,引发一次回流和重绘；
* 通过display:none来将节点脱离文档流，在修改完节点之后再显示，这样只有隐藏，显示两次。
* 使用cloneNode(true or false) 和 replaceChild 技术，引发一次回流和重绘；

3. 不要经常访问会引起浏览器flush队列的属性，如果你确实要访问，利用缓存

4. 让元素脱离动画流，减少回流的Render Tree的规模
```js
$("#block1").animate({left:50});
$("#block2").animate({marginLeft:50});
```

5. position:absolute,fixed 会将节点脱离文档流，避免整个dom tree重排

6. 移动通过translate来实现
