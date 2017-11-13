# 移动端布局解决方案
### 1、rem
* rem（font size of the root element）是指相对于根元素的字体大小的单位。简单的说它就是一个相对单位。看到rem大家一定会想起em单位；<br/>
* em（font size of the element）是指相对于父元素的字体大小的单位。它们之间其实很相似，只不过一个计算的规则是依赖根元素一个是依赖父元素计算
### 2、viewport
* viewport并非只是ios上的独有属性，在android、winphone上同样也有viewport。它们要解决的问题是相同的，即无视设备的真实分辨率，直接通过dpi，在物理尺寸和浏览器之间**重设分辨率**，这个分辨率和设备的分辨率无关。比如，你拿个3.5寸-320 * 480的iphone3 gs、3.5寸-640 * 960的iphone4或者9.7寸-1024*768的ipad2，虽然设备的分辨率不同,物理尺寸也不同，但你可以通过设置viewport让它们在浏览器里有相同的分辨率。比如说，你的网站是800px宽，你可以通过设置viewport的width=800，来让你的网站在这三个不同的设备上都刚好满屏显示你的网站。
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no" />
```
* 让viewport的宽度等于物理设备上的真实分辨率，不允许用户缩放。主流的web app都是这么设置的，它的作用其实是故意舍弃viewport，不缩放页面，这样dpi肯定和设备上的真实分辨率是一样的，不做任何缩放，网页会因此显得更高细腻。玩ps的同学应该都知道，当你将一张1000 * 1000的图片直接缩放至500 * 500分变成什么样，对吧？图片的失真一定逃不掉
* layout viewport---document.documentElement.clientWidth
* visual viewport---window.innerWidth
* ideal viewport---移动设备的理想viewport（只要在css中把某一元素的宽度设为ideal viewport的宽度(单位用px)，那么这个元素的宽度就是设备屏幕的宽度了，也就是宽度为100%的效果。ideal viewport 的意义在于，无论在何种分辨率的屏幕下，那些针对ideal viewport 而设计的网站，不需要用户手动缩放，也不需要出现横向滚动条，都可以完美的呈现给用户）
### 3、媒体查询
```html
<style>
  html {
    font-size: 32px;
  }
  
  @media (min-device-width: 375px) {
    font-size: 37.5px;
  }
  
  @media (min-device-width: 414px) {
    font-size: 41.4px;
  }
</style>
```
* 可能不会太精准，比如我的设备布局viewport可能是370px，这样只能使用320这一版本
* 响应式这种方式在国内很少有大型企业的复杂性的网站在移动端用这种方法去做，主要原因是工作大，维护性难，所以一般都是中小型的门户或者博客类站点会采用响应式的方法从web page到web app直接一步到位，因为这样反而可以节约成本，不用再专门为自己的网站做一个web app的版本
### 4、em
### 5、vv、vw
### 6、微信小程序rpx
### 7、流式布局
* 在页面布局的时候都是通过百分比来定义宽度，但是高度大都是用px来固定住，所以在大屏幕的手机下显示效果会变成有些页面元素宽度被拉的很长，但是高度还是和原来一样，实际显示非常的不协调，这就是流式布局的最致命的缺点
### 8、固定宽度做法
* 有些网站把页面设置成320的宽度，超出部分留白，这样做视觉，前端都挺开心，视觉在也不用被流式布局限制自己的设计灵感了，前端也不用在搞坑爹的流式布局。但是这种解决方案也是存在一些问题，例如在大屏幕手机下两边是留白的，还有一个就是大屏幕手机下看起来页面会特别小，操作的按钮也很小，手机淘宝首页起初是这么做的，但近期改版了，采用了rem。
