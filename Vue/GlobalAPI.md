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
  * Vue.nextTick<br/>Defer the callback to be executed after the next DOM update cycle. Use it immediately after you’ve changed some data to wait for the DOM update.
```html
// modify data
vm.msg = 'Hello';
// DOM not updated yet
Vue.nextTick(function () {
  // DOM updated
})
```
  * Vue.set<br/>Set a property on an object. If the object is reactive, ensure the property is created as a reactive property and trigger view updates. This is primarily used to get around the limitation that Vue cannot detect property additions.
```js
Vue.set(obj, 'key', '1');
```
  * Vue.directive
  * Vue.delete
  * Vue.filter
  * Vue.component
  * Vue.use
  * Vue.mixin
  * Vue.compile
  * Vue.version
