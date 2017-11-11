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
