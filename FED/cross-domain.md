# 跨域
## 什么是跨域
跨域，是指浏览器不能执行其他网站的脚本。它是由浏览器的**同源策略**造成的，是浏览器对JavaScript实施的安全限制  

同源策略限制了一下行为：  

* Cookie、LocalStorage 和 IndexDB 无法读取
* DOM 和 JS 对象无法获取
* Ajax请求发送不出去

所谓的同源是指，域名(主域名，子域名)、协议、端口均为相同
```
http://www.nealyang.cn/index.html 调用   http://www.nealyang.cn/server.php  非跨域

http://www.nealyang.cn/index.html 调用   http://www.neal.cn/server.php  跨域,主域不同

http://abc.nealyang.cn/index.html 调用   http://def.neal.cn/server.php  跨域,子域名不同

http://www.nealyang.cn:8080/index.html 调用   http://www.nealyang.cn/server.php  跨域,端口不同

https://www.nealyang.cn/index.html 调用   http://www.nealyang.cn/server.php  跨域,协议不同

localhost   调用 127.0.0.1 跨域
```
