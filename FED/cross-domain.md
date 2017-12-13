# 跨域
## 什么是跨域
跨域，是指浏览器不能执行其他网站的脚本。它是由浏览器的**同源策略**造成的，是浏览器对JavaScript实施的安全限制  

同源策略限制了一下行为：  

* Cookie、LocalStorage 和 IndexDB 无法读取
* DOM 和 JS 对象无法获取
* Ajax请求发送不出去

## 常见的跨域场景
所谓的同源是指，域名(主域名，子域名)、协议、端口均为相同
```
http://www.nealyang.cn/index.html 调用   http://www.nealyang.cn/server.php  非跨域

http://www.nealyang.cn/index.html 调用   http://www.neal.cn/server.php  跨域,主域不同

http://abc.nealyang.cn/index.html 调用   http://def.neal.cn/server.php  跨域,子域名不同

http://www.nealyang.cn:8080/index.html 调用   http://www.nealyang.cn/server.php  跨域,端口不同

https://www.nealyang.cn/index.html 调用   http://www.nealyang.cn/server.php  跨域,协议不同

localhost   调用 127.0.0.1 跨域
```

## 跨域的解决办法
### JSONP跨域(虽然这种方式非常好用，但是一个最大的缺陷是，只能够实现get请求)

sonp跨域其实也是JavaScript设计模式中的一种代理模式。在html页面中通过相应的标签从不同域名下加载静态资源文件是被浏览器允许的，所以我们可以通过这个“犯罪漏洞”来进行跨域。一般，我们可以动态的创建script标签，再去请求一个带参网址来实现跨域通信
```js
//原生的实现方式
let script = document.createElement('script');

script.src = 'http://www.nealyang.cn/login?username=Nealyang&callback=callback';

document.body.appendChild(script);

function callback(res) {  
  console.log(res);
}
```
当然，jquery也支持jsonp的实现方式
```js
$.ajax({
    url:'http://www.nealyang.cn/login',
    type:'GET',
    dataType:'jsonp',//请求方式为jsonp
    jsonpCallback:'callback',
    data:{
        "username":"Nealyang"
    }
})
```

### document.domain + iframe 跨域(这种跨域的方式最主要的是要求主域名相同)
### window.name + iframe 跨域
### location.hash + iframe 跨域
### postMessage跨域
### 跨域资源共享 CORS（目前主流的跨域解决方案）
CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。 它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制。  

**CORS需要浏览器和服务器同时支持**。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10。IE8+：IE8/9需要使用XDomainRequest对象来支持CORS。  

整个CORS通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，CORS通信与同源的AJAX通信没有差别，代码完全一样。浏览器一旦发现AJAX请求跨源，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。
因此，实现CORS通信的关键是服务器。**只要服务器实现了CORS接口，就可以跨源通信**。

### WebSocket协议跨域
### node代理跨域
### nginx代理跨域

