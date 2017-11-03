# 全局API
  * Vue.extend
```html
<div id=""></div>
<script>
  // create constructor
  var Profile = Vue.extend({
    template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
    data: function () {
      return {
        firstName: 'Walter',
        lastName: 'White',
        alias: 'Heisenberg'
      }
    }
  })
  // create an instance of Profile and mount it on an element
  new Profile().$mount('#mount-point')
</script>
```
  * Vue.nextTick
  * Vue.set
  * Vue.directive
  * Vue.delete
  * Vue.filter
  * Vue.component
  * Vue.use
  * Vue.mixin
  * Vue.compile
  * Vue.version
