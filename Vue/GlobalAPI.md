# 全局API
  * Vue.extend<br/>Create a “subclass” of the base Vue constructor. The argument should be an object containing component options. The special case to note here is the data option - it must be a function when used with Vue.extend().
```html
<div id="mount-point"></div>
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
