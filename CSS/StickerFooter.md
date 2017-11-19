# Sticker Footer 布局
## 什么是 Sticker Footer 布局
### 所谓 “Sticky Footer”，是指如果页面内容不足够长时，页脚固定在浏览器窗口的底部；如果内容足够长时，页脚固定在页面的最底部。但如果网页内容不够长，置底的页脚就会保持在浏览器窗口底部。
## 几种实现方法：
### 1、内容部分设置 min-height: 100%; 且 margin-bottom 设置为负数，值等于footer的高度
```html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
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
</html>
```
