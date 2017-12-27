# 前端本地存储 （cookie、localStorage、sessionStorage）

## cookie
网络早期最大的问题之一是如何管理状态。简而言之，服务器无法知道两个请求是否来自同一个浏览器

### 特征
1. 不同的浏览器存放的cookie位置不一样，也是不能通用的
2. cookie的存储是以域名形式进行区分的，不同的域名下存储的cookie是独立的
3. 我们可以设置cookie生效的域（当前设置cookie所在域的子域），也就是说，我们能够操作的cookie是当前域预计当前域下的所有子域
4. 一个域名下存放的cookie的个数是有限制的，不同的浏览器存放的个数不一样，一般为20个
5. 每个cookie存放的内容大小也是有限制的，不同的浏览器存放大小不一样，一般为4KB
6. cookie也可以设置过期的时间，默认是回话结束的时候，当时间到期自动销毁

### cookie值既可以设置，也可以读取

### 一、设置

#### 客户端设置

```js
// 设置cookie，并且设置了生效域
document.cookie = "usernamne=lyy;domain=baike.baidu.com"
```

**注意：** 客户端可以设置cookie的下列选项：`expires`、`domain`、`path`、`secure`（有条件：只有在https协议的网页中，客户端设置secure类型的cookie才能成功），但无法设置 `HttpOnly` 选项

#### 服务端设置

不关你是请求一个资源文件（如html/js/css/图片），还是发送一个ajax请求，服务端都会返回response，而 Response Header 中有一项叫做 `set-cookie` ，是服务端专门用来设置cookie的

```
Set-Cookie 消息头是一个字符串，其格式如下（中括号中的部分是可选的）
Set-Cookie: value[; expires=date][; do main=domain][; path=path][; secure]
```

**注意：** 一个set-Cookie字段只能设置一个cookie，当你要想设置多个cookie，需要添加同样多的set-cookie字段。  
服务端可以设置cookie的所有选项：expires、domain、path、secure、HttpOnly，通过 Set-Cookie 指定的这些可选项只会在浏览器端使用，而不会被发送至服务器端

### 二、读取

我们通过 document.cookie 来获取当前网站下的cookie的时候，得到的字符串形式的值，它包含了当前网站下所有的cookie（为了避免跨域脚本攻击（xss），这个方法只能获取非 HttpOnly 类型的cookie）。它会把所有的 cookie 通过一个分号 + 空格的形式串联起来,例如 "username=lyy; job=coding"

### 三、修改

要想修改一个cookie，只需要重新赋值就行，旧的值会被新的值覆盖。但要注意一点，在设置新cookie时，path/domain这几个选项一定要和旧cookie保持一样。否则不会修改旧制，而是添加了一个新的cookie

### 四、删除

把要删除的cookie的过期时间设置成已过去的时间，path/domain。。。这几个选项一定要和旧cookie保持一样

**注意：** 如果只设置一个值，那么算cookie中的value；设置的两个cookie，key值如果设置的相同，下面的也会把上面的覆盖

## localStorage
HTML5新方法，IE8及以上浏览器兼容

### 特点

* 生命周期：持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的
* 存储的信息在同一域中是共享的
* 在本页操作（新增、修改、删除）了 localStorage 的时候，本页面不会触发 storage 事件，但是别的页面会触发 storage 事件
* 大小： 一版5M（跟浏览器厂商有关系）
* 在非IE下的浏览器中可以本地打开。IE浏览器要在服务器中打开
* localStorage 本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，导致页面变卡
* localStorage 受同源策略限制

```js
// 设置
localStorage.setItem('local', 123);

// 读取
localStorage.getItem('local');

// 删除
localStorage.remove('local');

// 一次性清除
localStorage.clear();
```

## sessionStorage

跟localStorage差不多，也是本地存储，会话本地存储

### 特点

* 用于本地存储一个会话中的数据，这些数据只有在同一个会话中的页面才能访问，并且当会话结束后数据也随之销毁。因此 sessionStorage 不是一种持久化的本地存储，仅仅是会话级别的存储。
* 刷新页面，数据仍然存在
* 关闭标签页，清除数据

## cookie、localStorage、sessionStorage区别

* 相同：都是在（浏览器端）存储数据
* 不同：
1. cookie 的数据会在每一次发送http请求时被携带；另外两个不会
2. localStorage 只要在相同的协议、相同的主机、相同的端口下，就能读取/修改到同一份数据
3. sessionStorage 比 localStorage 更严苛，要在同一窗口（也就是浏览器的同一标签页）下
4. localStorage永久，sessionStorage会话
