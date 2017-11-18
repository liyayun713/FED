# 不定宽高垂直水平居中
### 一、通过 transform: translate 实现
```css
div {
  position: absolute;
  top: 50%
  left: 50%
  -webkit-transform: translate(-50%, -50%)
  background: #eee
}
```
* 先把元素设定为绝对定位，
* 然后通过 top 和 left 把元素的左上点移动到屏幕的中间，
* 最后通过 transform 属性，根据元素自身大小，相对向左和向上移动自身宽高的50%，从而实现了不定宽高元素的水平垂直居中
### 二、通过 display: flex 实现
```css
div {
  display: flex;
  justify-content: center;
  align-item: center
}
```
* 设置父级元素 display 为 flex
* justify-content 设定子元素水平居中
* align-items 设定子元素垂直居中
