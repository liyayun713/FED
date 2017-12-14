# Flex弹性盒子布局
## 一、Flex 布局是什么？
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。  

任何一个容器都可以指定为 Flex 布局。  

```css
.box{
  display: flex;
}
```

行内元素也可以使用 Flex 布局。  

```css
.box{
  display: inline-flex;
}
```

Webkit 内核的浏览器，必须加上-webkit前缀。  

```css
.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
```

注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。  

## 二、基本概念
