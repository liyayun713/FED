# 创建对象的几种方法
### 对象字面量
```js
var person = {};    

person.name = 'ifcode';
person.setName = function(theName) {
   person.name = theName;
}
console.log(person);
```

### 一、工厂模式
1. 在函数中定义对象,并定义对象的各种属性,虽然属性可以为方法，但是建议将属性为方法的属性定义到函数之外，这样可以避免重复创建该方法
2. 引用该对象的时候，这里使用的是 var x = Parent()而不是 var x = new Parent();因为后者会可能出现很多问题（前者也成为工厂经典方式,后者称之为混合工厂方式），不推荐使用new的方式使用该对象
3. 在函数的最后返回该对象
4. 不推荐使用这种方式创建对象，但应该了解 

```js
var lev = function() { 
  return "脚本之家"; 
}; 

function Parent() { 
  var Child = new Object(); 
  Child.name="脚本"; 
  Child.age="4"; 
  Child.lev=lev; 
  return Child; 
}; 
var x = Parent();
console.log(x);
console.log(x.name);
console.log(x.lev());
```

### 二、构造函数模式
1. 与工厂方式相比，使用构造函数方式创建对象，无需再函数内部重建创建对象，而使用this指代，并而函数无需明确return
2. 同工厂模式一样，虽然属性的值可以为方法，扔建议将该方法定义在函数之外
3. 同样的，不推荐使用这种方式创建对象，但仍需要了解

```js
var lev = function() { 
  return "脚本之家"; 
}; 
function Parent(){ 
  this.name = "脚本";
  this.age = "30"; 
  this.lev = lev; 
}; 
var x = new Parent();
console.log(x);
console.log(x.name);
console.log(x.lev()); 
```

要创建person的实例，必须使用new操作符，以这种方式调用构造函数实际上会经历4个步骤： 
1. 创建一个`新对象` 
2. 将构造函数的`作用域`赋给新对象 
3. `执行`构造函数中的代码 
4. `返回`新对象 

### 三、原型模式 --- 关键词：共享

*我们创建的每个函数都有一个prototype属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。prototype是通过调用构造函数而创建的那个对象实例的对象原型，使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法*

1. 函数中不对属性进行定义
2. 利用prototype属性对属性进行定义
3. 同样的，不推荐使用这样方式创建对象

```js
var lev=function(){ 
  return "脚本之家";
};

function Parent(){}; 

Parent.prototype.name = "李小龙";
Parent.prototype.age = "30"; 
Parent.prototype.lev = lev;

var x = new Parent();

console.log(x);
console.log(x.name);
console.log(x.lev());
```
### 四、组合使用构造函数和原型模式
1. 该模式是指混合搭配使用构造函数方式和原型方式
2. 将所有属性不是方法的属性定义在函数中（构造函数方式）
3. 将所有属性值为方法的属性利用prototype在函数之外定义（原型方式）
4. `这样每个实例都有自己的一份实例属性的副本，又同时共享着对方法的引用，最大限度的节省了内存`

```js
var lev = function () {
  return '混合模式';
}

function MixModel() {
  this.name = '李四';
  this.age = 18;
}

MixModel.prototype.lev = lev;

var obj = new MixModel();

console.log(obj);
console.log(obj.name);
console.log(obj.lev());
```
### 五、动态原型方式
1. 动态原型方式可以理解为混合构造函数，原型方式的一个特例
2. 该模式中,属性为方法的属性直接在函数中进行了定义，但是因为
```js
if (typeof Parent._lev == "undefined") { 
  Parent._lev=true;
}
```
从而保证创建该对象的实例时，属性的方法不会被重复创建  

3. 推荐使用这种模式
```js
function Parent(){ 
  this.name="脚本";
  this.age=4;

  if(typeof Parent._lev == "undefined"){
    Parent.prototype.lev = function(){
      return this.name;
    }
    Parent._lev = true;
  }
}; 

var x = new Parent();

console.log(x);
```
