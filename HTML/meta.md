# 常用meta标签
### 1、屏幕的缩放---viewport
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
```
### 2、format-detection忽略电话号码和邮箱
* 忽略页面中的数字识别为电话号码
```html
<meta name="format-detection" content="telephone=no" />
```
* 忽略页面中的邮箱格式为邮箱
```html
<meta name="format-detection" content="email=no" />
```
```html
<meta name="format-detection" content="telphone=no, email=no"/>  
```
### 3、声明文档的使用编码
```html
<meta charset="utf-8" />
<!-- 用以说明主页制作所使用的文字以及语言-->
<meta http-equiv="content-type" content="text/html; charset=utf-8" />
```
### 4、优先使用IE最先版本和Chrome
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge, chrome=1" />
```
### 5、SEO的优化，页面描述、页面关键字
```html
<meta name="description" content="..." />
<meta name="keywords" content="..." />
```
### 6、IOS系统
* 开启对Web App的支持（网站开启对web app程序的支持，其实意思就是删除默认的苹果工具栏和菜单栏，开启全屏显示）
```html
<meta name="apple-mobile-web-app-capable" content="yes" />
```
* 改变顶部状态栏的颜色（在 web app 应用下状态栏的颜色，默认值为白色，可以定为 black（黑色）和 black-translucent（灰色半透明））
```html
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```
* 添加到主屏幕后，全屏显示
```html
<meta name="apple-touch-fullscreen" content="yes">
```
### 7、content的取值为webkit,ie-comp,ie-stand之一，区分大小写，分别代表用webkit内核，IE兼容内核，IE标准内核
```html
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```
### 8、禁止浏览器缓存（是用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出）
```html
<meta http-equiv="pragram" content="no-cache"> 
```
