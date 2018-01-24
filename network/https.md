# HTTPS
![](http://liushaoqing.me/uploads/https/https.jpg)

## http 通信有什么问题？
1. 可能被窃取
* HTTP 本身不具备加密的功能,HTTP 报文使用明文方式发送
* 由于互联网是由联通世界各个地方的网络设施组成,所有发送和接收经过某些设备的数据都可能被截获或窥视。(例如大家都熟悉的抓包工具:Wireshark),即使经过加密处理,也会被窥视是通信内容,只是可能很难或者无法破解出报文的信息而已

2. 认证问题
* 无法确认你发送到的服务器就是真正的目标服务器(可能服务器是伪装的)
* 无法确定返回的客户端是否是按照真实意图接收的客户端(可能是伪装的客户端)
* 无法确定正在通信的对方是否具备访问权限,Web 服务器上某些重要的信息，只想发给特定用户
* 即使是无意义的请求也会照单全收。无法阻止海量请求下的 DoS 攻击（Denial of Service，拒绝服务攻击）

3. 可能被篡改
* 请求或响应在传输途中，遭攻击者拦截并篡改内容的攻击被称为中间人攻击（Man-in-the-Middle attack，MITM）

## HTTPS如何解决上述三个问题
HTTPS 只是在通信接口部分用 TLS（Transport Layer Security）协议代替而已。

![](http://liushaoqing.me/uploads/https/https1.png)

SSL 和 TLS 的区别:

> 传输层安全性协议（英语：Transport Layer Security，缩写作 TLS），及其前身安全套接层（Secure Sockets Layer，缩写作 SSL）是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。网景公司（Netscape）在1994年推出首版网页浏览器，网景导航者时，推出HTTPS协议，以SSL进行加密，这是SSL的起源。IETF将SSL进行标准化，1999年公布第一版TLS标准文件。随后又公布RFC 5246 （2008年8月）与 RFC 6176 （2011年3月）。以下就简称SSL

TLS 是 SSL 的标准. HTTPS 就是 HTTP + SSL

![](http://liushaoqing.me/uploads/https/https_http.png)

## SSL 协议
SSL 协议的实现需要用到的几类算法

### 对称加密
常用的加密算法: DES、AES、RC2、RC4

优点：算法公开、计算量小、加密速度快、加密效率高

缺点：交易双方都使用同样钥匙，安全性得不到保证

![](http://liushaoqing.me/uploads/https/https2.png)

### 非对称加密
常用的非对称加密算法: RSA、DSA、Diffie-Hellman

优点:安全性高

缺点:速度慢

![](http://liushaoqing.me/uploads/https/https3.png)

### 完整性验证算法
HASH算法：MD5、SHA1、SHA256

用作校验消息的完整性

![](http://liushaoqing.me/uploads/https/tls_ssl.png)

### SSL协议构成
1. 第一层是Record Protocol, 用于定义传输格式。
2. 第二层Handshake Protocol,它建立在SSL记录协议之上,用于在实际的数据传输开始前，通讯双方进行身份认证、协商加密算法、交换加密密钥等。

![](http://liushaoqing.me/uploads/https/ssl_layout.png)

> 工作方式:
> * 客户端使用非对称加密与服务器进行通信，实现身份验证并协商对称加密使用的密钥，
> * 然后采用协商密钥对信息进行加密通信，不同的节点之间采用的对称密钥不同，从而可以保证对称密钥的安全。

### SSL密钥协商的过程如下
![](http://liushaoqing.me/uploads/https/https_ssl.svg)

1. client_hello 过程
客户端发起请求，以明文传输请求信息，包含版本信息，加密套件候选列表，压缩算法候选列表，随机数，扩展字段等信息，相关信息如下：

* 版本信息: 支持的最高TSL协议版本version，从低到高依次 SSLv2 SSLv3 TLSv1 TLSv1.1 TLSv1.2，当前基本不再使用低于 TLSv1 的版本
* 加密套件候选列表(cipher suite): 认证算法 Au (身份验证)、密钥交换算法 KeyExchange(密钥协商)、对称加密算法 Enc (信息加密)和信息摘要 Mac(完整性校验);
* 压缩算法候选列表:支持的压缩算法 compression methods 列表，用于后续的信息压缩传输;
* 随机数:随机数就是上图里的RNc,用于后续生成协商密钥;
* 协商数据:支持协议与算法的相关参数以及其它辅助信息等，常见的 SNI 就属于扩展字段，后续单独讨论该字段作用。

2. server_hello 过程
* 服务端返回协商的信息结果，包括选择使用的协议版本version，选择的加密套件 cipher suite，选择的压缩算法 compression method、随机数 RNs等，其中随机数用于后续的密钥协商;
* 服务器证书链,用于身份校验和密钥交换
* 通知客户端server-hello 结束,请求客户端的证书和密钥

3. 证书校验，协商最后通信密钥
> a. 客户端验证服务端证书的合法性，如果验证通过才会进行后续通信，否则根据错误情况不同做出提示和操作，合法性验证包括如下：
> 
> * 证书链的可信性 trusted certificate path
> * 证书是否吊销 revocation
> * 有效期 expiry date，证书是否在有效时间范围;
> * 域名 domain，核查证书域名是否与当前的访问域名匹配，匹配规则后续分析;
> 
> b. 客户端发送客户端证书,公钥服务端验证(过程同客户端验证)
> 
> c. 客户端hash所有之前的消息,发送hash值和摘要,用客户端的私钥加密发送给服务端,服务端用客户端的公钥解密,验证了服务端获取的客户端的公钥和算法是正确的
> 
> d. 客户端生成pms,用服务端的公钥加密加密后发送给服务端
> 
> e. 客户端和服务端同时计算出最终会话密钥(MS)

4. 验证协商密钥
a. Client发送ChangeCipherSpec，指示Server从现在开始发送的消息都是加密过的
b. Client发送Finishd，包含了前面所有握手消息的hash，可以让server验证握手过程是否被第三方篡改
c. 服务端发送ChangeCipherSpec，指示Client从现在开始发送的消息都是加密过的
d. Server发送Finishd，包含了前面所有握手消息的hash，可以让client验证握手过程是否被第三方篡改，并且证明自己是Certificate密钥的拥有者，即证明自己的身份

### HTTPS完整建立连接过程,如下图
1. 首先建立tcp 握手连接
2. 进行ssl 协议的握手密钥交换(Handshake protocal)
3. 然后通过共同约定的密钥开始通信

![](http://liushaoqing.me/uploads/https/https_protocal.png)

### 上文说到的证书是个什么玩意儿
![](http://liushaoqing.me/uploads/https/zhengshu_brower.png)

#### 证书的作用就是,我和服务端通信,我怎么知道这个服务端是我要真正通信的服务端呢. 打个不恰当的比方:

你在某宝购物,到了结算页面,你消费了100万,输入银行卡账号和密码付款,但是当你付款结束以后,你发现账户少了100万,但是账户页面还是显示未付款,你去打某宝客服,客服说你被别人盗号了100万没支付到我某宝,注意：这里面存在两种可能性

1. 一个是有可能遭到了中间人攻击(用户名和密码被黑客截获)
2. 某宝收了你的钱，假装不承认,(抵赖)

![](http://liushaoqing.me/uploads/https/https_gj.png)

#### 申请和发放证书流程如下：
![](http://liushaoqing.me/uploads/https/zhengshu.png)

1. 服务方 Server 向第三方机构CA提交公钥、组织信息、个人信息(域名)等信息并申请认证;

2. CA通过线上、线下等多种手段验证申请者提供信息的真实性，如组织是否存在、企业是否合法，是否拥有域名的所有权等;

3. 如信息审核通过，CA会向申请者签发认证文件-证书。证书包含以下信息：申请者公钥、申请者的组织信息和个人信息、签发机构 CA的信息、有效时间、证书序列号等信息的明文，同时包含一个签名; 签名的产生算法：首先，使用散列函数计算公开的明文信息的信息摘要，然后，采用 CA的私钥对信息摘要进行加密，密文即签名;

4. 客户端 Client 向服务器 Server 发出请求时，Server 返回证书文件;

5. 客户端 Client 读取证书中的相关的明文信息，采用相同的散列函数计算得到信息摘要，然后，利用对应 CA的公钥解密签名数据，对比证书的信息摘要，如果一致，则可以确认证书的合法性，即公钥合法;

6. 客户端还会验证证书相关的域名信息、有效时间等信息; 客户端会内置信任CA的证书信息(包含公钥)，如果CA不被信任，则找不到对应 CA的证书，证书也会被判定非法。

#### 证书链
![](http://liushaoqing.me/uploads/https/zhengshulian.png)

1. 服务器证书 server.pem 的签发者为中间证书机构 inter，inter 根据证书 inter.pem 验证 server.pem 确实为自己签发的有效证书
2. 中间证书 inter.pem 的签发 CA 为 root，root 根据证书 root.pem 验证 inter.pem 为自己签发的合法证书;
3. 客户端内置信任 CA 的 root.pem 证书，因此服务器证书 server.pem 的被信任。

> 服务器证书、中间证书与根证书在一起组合成一条合法的证书链，证书链的验证是自下而上的信任传递的过程。
