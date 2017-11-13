# keep-alive组件的使用及其原理
### 它能够不活动的组件实例保存在内存中，而不是直接将其销毁，它是一个抽象组件，不会被渲染到真实DOM中，也不会出现在父组件链中。它提供了include与exclude两个属性，允许组件有条件地进行缓存。
```html
<keep-alive>
  <component></component>
</keep-alive>
```
