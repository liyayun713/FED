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
