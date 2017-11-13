# 移动端布局解决方案
### 1、rem
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
