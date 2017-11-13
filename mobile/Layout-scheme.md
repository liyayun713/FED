# 移动端布局解决方案
### 1、rem
rem（font size of the root element）是指相对于根元素的字体大小的单位。简单的说它就是一个相对单位。看到rem大家一定会想起em单位；<br/>
em（font size of the element）是指相对于父元素的字体大小的单位。它们之间其实很相似，只不过一个计算的规则是依赖根元素一个是依赖父元素计算。
### 2、viewport
### 3、媒体查询
```html
<style>
  html {
    font-size: 32px;
  }
  
  @media (min-device-width: 375px) {
    font-size: 37.5px;
  }
  
  @media (min-device-width: 414px) {
    font-size: 41.4px;
  }
</style>
```
可能不会太精准，比如我的设备布局viewport可能是370px，这样只能使用320这一版本
### 4、em
### 5、vv、vw
### 6、微信小程序rpx
