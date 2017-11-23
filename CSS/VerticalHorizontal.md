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
### 三、通过 绝对定位(top、bottom、left、right均为0) + margin(auto)
```css
.father {
    width:200px;
    height:300px;
    background: yellow;
    position: relative;
}
.child{
    width:50%;/*这里为了实体化，给了宽高，但是宽高可以任意改变，就是所谓的不定宽高*/
    height:50%;
    position: absolute;
    left:0;
    top:0;
    right:0;
    bottom:0;
    background: red;
    margin: auto; /*重点就是他*/
}
```
