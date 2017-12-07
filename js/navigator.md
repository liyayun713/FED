# window.navigator
### The Window.navigator read-only property returns a reference to the Navigator object, which can be queried for information about the application running the script.
 
### 移动端项目中浏览器判断
* UC浏览器：UCBrowser
* 微信：MicroMessenger
* 百度 App：baiduboxapp
* 百度浏览器：baidubrowser
* QQ浏览器：MQQBrowser
* 搜狗浏览器：SogouMobileBrowser
* 猎豹浏览器：LieBaoFast
* QQ App：MQQBrowser
* 傲游浏览器：Maxthon
* 360浏览器：无


### navigator.userAgent
```js
"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36"

```

```js
var sBrowser, sUsrAg = navigator.userAgent;

if(sUsrAg.indexOf("Chrome") > -1) {
    sBrowser = "Google Chrome";
} else if (sUsrAg.indexOf("Safari") > -1) {
    sBrowser = "Apple Safari";
} else if (sUsrAg.indexOf("Opera") > -1) {
    sBrowser = "Opera";
} else if (sUsrAg.indexOf("Firefox") > -1) {
    sBrowser = "Mozilla Firefox";
} else if (sUsrAg.indexOf("MSIE") > -1) {
    sBrowser = "Microsoft Internet Explorer";
}

alert("You are using: " + sBrowser);
```
