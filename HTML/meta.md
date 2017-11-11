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
