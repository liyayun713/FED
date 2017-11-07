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
```js
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
  * Vue.directive<br/>Register or retrieve a global directive.
  * Vue.delete<br/>Delete a property on an object. If the object is reactive, ensure the deletion triggers view updates. This is primarily used to get around the limitation that Vue cannot detect property deletions, but you should rarely need to use it.
  * Vue.filter<br/>Register or retrieve a global filter.
  * Vue.component<br/>Register or retrieve a global component. Registration also automatically sets the component’s name with the given id.
  * Vue.use<br/>Install a Vue.js plugin. If the plugin is an Object, it must expose an install method. If it is a function itself, it will be treated as the install method. The install method will be called with Vue as the argument.<br/>When this method is called on the same plugin multiple times, the plugin will be installed only once.
  * Vue.mixin<br/>Apply a mixin globally, which affects every Vue instance created afterwards. This can be used by plugin authors to inject custom behavior into components. Not recommended in application code.
  * Vue.compile<br/>Compiles a template string into a render function. Only available in the full build.
```js
var res = Vue.compile('<div><span>{{ msg }}</span></div>')
new Vue({
  data: {
    msg: 'hello'
  },
  render: res.render,
  staticRenderFns: res.staticRenderFns
})
```
  * Vue.version<br/>Provides the installed version of Vue as a string. This is especially useful for community plugins and components, where you might use different strategies for different versions.
```js
var version = Number(Vue.version.split('.')[0])
if (version === 2) {
  // Vue v2.x.x
} else if (version === 1) {
  // Vue v1.x.x
} else {
  // Unsupported versions of Vue
}
```
