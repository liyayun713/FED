# 浏览器http缓存
>  Web缓存可以分为这几种：**浏览器缓存、CDN缓存、服务器缓存、数据库数据缓存** 。因为可能会直接使用副本免于重新发送请求或者仅仅确认资源没变无需重新传输资源实体，`Web缓存可以减少延迟加快网页打开速度`、`重复利用资源减少网络带宽消耗`、`降低请求次数或者减少传输内容从而减轻服务器压力`。

这篇文章主要讨论和前端密切相关的**浏览器HTTP缓存机制**。浏览器HTTP缓存可以分为`强缓存`和`协商缓存`。

强缓存和协商缓存最大也是最根本的区别是：

* 强缓存命中的话不会发请求到服务器（比如chrome中的200 from memory cache）
* 协商缓存一定会发请求到服务器，通过资源的请求首部字段验证资源是否命中协商缓存，如果协商缓存命中，服务器会将这个请求返回，但是不会返回这个资源的实体，而是通知客户端可以从缓存中加载这个资源（304 not modified）。

## 常用字段介绍
### Pragma
该字段只有`no-cache`一个可选值，会通知浏览器不直接使用缓存，要求向服务器发请求校验新鲜度。因为它优先级最高，当存在时一定不会命中强缓存。

### Cache-Control
|指令|参数|说明|
|----|----|----|
|private|无|表明响应只能被单个用户缓存，不能作为共享缓存（即代理服务器不能缓存它）|
|public|可省略|表明响应可以被任何对象（包括：发送请求的客户端，代理服务器，等等）缓存|
|no-cache|可省略|缓存前必需确认其有效性|
|no-store|无|不缓存请求或响应的任何内容|
|max-age=[s]|必需|响应的最大值|

* max-age（单位为s）
设置缓存的存在时间，相对于发送请求的时间。只有响应报文首部设置Cache-Control为非0的max-age或者设置了大于请求日期的Expires（下文会讲）才有可能命中强缓存。当满足这个条件，同时响应报文首部中Cache-Control不存在no-cache、no-store且请求报文首部不存在Pragma字段，才会真正命中强缓存。

![](https://pic1.zhimg.com/80/v2-91b2b09d4a3a04dbd3b7fd81cade1b1e_hd.jpg)

如图所见，来自服务器端的 response headers 的 Headers 中有 cache-control: max-age=93312000，这就是告诉浏览器这个资源的生存时间，在这个时间以内，浏览器不需要向服务器端再做任何确认，直接使用即可。下面我们也可以看到 request headers 一栏是空的。因为浏览器根本没有发出请求，这里显示的 response headers 是之前的请求中缓存的。

* no-cache
表示请求必须先与服务器确认缓存的有效性，**如果有效才能使用缓存（协商缓存）**，无论是响应报文首部还是请求报文首部出现这个字段均一定不会命中强缓存。Chrome硬性重新加载（Command+shift+R）会在请求的首部加上Pragma：no-cache和Cache-Control：no-cache。

* no-store
表示禁止浏览器以及所有中间缓存存储任何版本的返回响应，一定不会出现强缓存和协商缓存，适合个人隐私数据或者经济类数据。

* public
表明响应可以被浏览器、CDN等等缓存。
* private

响应只作为私有的缓存，不能被CDN等缓存。如果要求HTTP认证，响应会自动设置为private。

### Expires
Expires是一个响应首部字段，它指定了一个日期/时间，在这个时间/日期之前，HTTP缓存被认为是有效的。无效的日期比如0，表示这个资源已经过期了。**如果同时设置了Cache-Control响应首部字段的max-age，则Expires会被忽略**。它也是HTTP/1.1之前版本遗留的通用首部字段，仅作为于HTTP/1.0的向后兼容而使用。

我们注意到在缓存的 response headers 里还有一个 expires: Sat, 24 Aug 2019 09:03:00 GMT 字段。**这个字段的意义实际上和 cache-control: max-age 的效果是相似的，在指定的时间之前浏览器都可以认为缓存是有效的。但当两个字段同时存在时，expires 会被 cache-control 覆盖**。

那么为什么知乎要同时设置两个字段呢？由于 expires 是 HTTP/1.0 定义的而 cache-control 是 HTTP/1.1 定义的，我猜测可能是为了保持尽可能大的兼容性（待考证）。

### Last-Modified/If-Modified-Since
**除了文件特征码之外也可以通过上次修改时间，服务器端返回资源时通过 Last-Modified 携带资源修改时间，浏览器通过 If-Modified-Since 携带缓存中的资源的修改时间。**

* If-Modified-Since是一个请求首部字段，并且只能用**在GET或者HEAD请求中**。
* Last-Modified是一个响应首部字段，包含服务器认定的资源作出修改的日期及时间。

当带着If-Modified-Since头访问服务器请求资源时，服务器会检查Last-Modified，如果Last-Modified的时间早于或等于If-Modified-Since则会返回一个不带主体的304响应，否则将重新返回资源。

### ETag/If-None-Match
知乎采用的是 ETag 来判断缓存是否有效，服务器端会在 response headers 中返回 ETag（文件的 hash）：

```
ETag:"2afd9676ae9046ed99dedd4635bb6e4a"
```

而当资源改变时 ETag 也会发生改变。浏览器在发起请求时在 If-None-Match字段携带缓存的 ETag：

```
If-None-Match:"2afd9676ae9046ed99dedd4635bb6e4a-gzip"
```

服务器接到请求后如果一致（即资源没有修改），则返回 304 Not Modified，否则返回新的资源（200）

* ETag是一个响应首部字段，它是根据实体内容生成的一段hash字符串，标识资源的状态，由服务端产生。
* If-None-Match是一个条件式的请求首部。如果请求资源时在请求首部加上这个字段，值为之前服务器端返回的资源上的ETag，则当且仅当服务器上没有任何资源的ETag属性值与这个首部中列出的时候，服务器才会返回带有所请求资源实体的200响应，否则服务器会返回不带实体的304响应。
* ETag优先级比Last-Modified高，同时存在时会以ETag为准。

#### 因为ETag的特性，所以相较于Last-Modified有一些优势：
1. 某些情况下服务器无法获取资源的最后修改时间
2. 资源的最后修改时间变了但是内容没变，使用ETag可以正确缓存
3. 如果资源修改非常频繁，在秒以下的时间进行修改，Last-Modified只能精确到秒

Last-Modified 有个缺点就是它是精确到秒的，如果一秒中资源多次服务器不会感知到缓存失效，但这不是一个常见的需求。

而一般不推荐使用 ETag，原因有几点

* Last-Modified 的缺点基本可以忽略不计
* ETag 本身需要消耗 CPU，而它的优先级比 Last-Modified 高，当它存在时服务器无论 Last-Modified 是否存在都会使用它判断
* ETag 在**分布式系统中生成的值可能不一样，会导致缓存失效**

### 整体流程
![](https://user-gold-cdn.xitu.io/2018/1/23/161233e6685e5e73?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
