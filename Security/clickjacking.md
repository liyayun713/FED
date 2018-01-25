# 点击劫持 Clickjacking
点击劫持，英文名clickjacking，也叫UI覆盖攻击，攻击者会利用一个或多个透明或不透明的层来诱骗用户支持点击按钮的操作，而实际的点击确实用户看不到的一个按钮，从而达到在用户不知情的情况下实施攻击。

这种攻击方式的关键在于可以实现页中页的 `<iframe />` 标签，并且可以使用css样式表将他不可见

**大概有两种方式：**

* 攻击者使用一个透明 iframe，覆盖在一个网页上，然后诱使用户在该页面上进行操作，此时用户将在不知情的情况下点击透明的 iframe 页面；
* 攻击者使用一张图片覆盖在网页，遮挡网页原有的位置含义。

![](https://user-gold-cdn.xitu.io/2017/9/22/ba3a34f60ca270ae31ffb2cb24b7a29a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

目前，clickjacking还算比较冷门，很多安全意识不强的网站还未着手做clickjacking的防范。这是很危险的

### 防范
防止点击劫持有两种主要方法：

1. X-FRAME-OPTIONS
X-FRAME-OPTIONS HTTP 响应头是用来给浏览器指示允许一个页面可否在<frame>, <iframe> 或者 <object> 中展现的标记。网站可以使用此功能，来确保自己网站内容没有被嵌到别人的网站中去，也从而避免点击劫持的攻击。

2. 顶层判断
```js
function locationTop(){
  if (top.location != self.location) {
     top.location = self.location; return false;
  }
  return true; 
 }
locationTop();
```

可轻易破解，意义不大

```js
// 破解：
// 顶层窗口中放入代码
var location = document.location;
//或者
var location = "";
```
