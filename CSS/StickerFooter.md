# Sticker Footer 布局
## 什么是 Sticker Footer 布局
### 所谓 “Sticky Footer”，是指如果页面内容不足够长时，页脚固定在浏览器窗口的底部；如果内容足够长时，页脚固定在页面的最底部。但如果网页内容不够长，置底的页脚就会保持在浏览器窗口底部。
## 几种实现方法：
### 1、内容部分设置 min-height: 100%; 且 margin-bottom 设置为负数，值等于footer的高度
```html
<head>
	<style>
		html, body {
			height: 100%;
			margin: 0;
		}
		.wrapper {
			min-height: 100%;
			/* 等于footer的高度 */
			margin-bottom: -50px;
		}
		.footer,
		.push {
			height: 50px;
			background: #000;
		}
	</style>
</head>
<body>
	<div class="wrapper">
		<div class="push"></div>
	</div>
	<footer class="footer"></footer>
</body>
```
### 2、父元素设置 min-height: 100$; 且footer设置 margin-top: -50%;
```html
<body>
  <div class="content">
    <div class="content-inside">
      content
    </div>
  </div>
  <footer class="footer"></footer>
</body>
```
```html
<style>
	html, body {
		height: 100%;
		margin: 0;
	}
	.content {
		min-height: 100%;
	}
	.content-inside {
		padding: 20px;
		padding-bottom: 50px;
	}
	.footer {
		height: 50px;
		margin-top: -50px;
	}
</style>
```
### 3、使用flexbox弹性盒子布局
```html
<body>
  <div class="content">
    content
  </div>
  <footer class="footer"></footer>
</body>
```
```html
<style>
	html {
		height: 100%;
	}
	body {
		min-height: 100%;
		display: flex;
		flex-direction: column;
	}
	.content {
		flex: 1;
	}
</style>
```
### 4、绝对定位，footer设置 position: absolute; bottom: 0; height: 100px; 父元素设置最小高度 min-height: 100%; padding-bottom: 100px;
