# event.target 和 event.currentTarget

首先本质区别：
* event.target返回触发事件的元素
* event.currentTarget返回绑定事件的元素

### event.target返回的是点击的元素节点

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta charset="utf-8">
</head>
<body>
	<div>
		<ul id="ul">
			ul
			<li>li1<a href="#">a1</a></li>
			<li>li2<a href="#">a2</a></li>
			<li>li3<a href="#">a3</a></li>
		</ul>
	</div>
	<script>
		var ul = document.getElementById('ul');
		ul.onclick = function (e) {
			var target = e.target;
			var name = target.nodeName;
			console.log('你点击了：' + name);
			e.preventDefault();
		}
	</script>
</body>
</html>
```

当我点击哪个元素时，`event.target` 返回的是点击的元素节点，我们可以用返回的节点使用一些DOM对象上的一些操作。这里event.preventDefault，是用来阻止点击a默认跳转，刷新页面导致结果不能输出来的一个作用。

### event.currentTarget的作用是什么呢，我觉得他和this 的作用是差不多的，始终返回的是绑定事件的元素

```js
var ul = document.getElementById('ul');
ul.onclick = function (e) {
    console.log(e.currentTarget);   // 点击到ul时，返回绑定的ul
    var target = e.target;
    var currentTarget = e.currentTarget;
    var name = target.nodeName;
    console.log('你点击了：' + name);
    e.preventDefault();
}
```

### 实际使用中target的妙用---事件委托
target事件委托的定义：本来该自己干的事，但是自己不干，交给别人来干。比如上面的例子中，应该是ul li a 来监控自身的点击事件，但是li a自己不监控这个点击事件了，全部交给li父节点和a祖父节点ul来监控自己的点击事件。一般用到for循环遍历节点添加事件的时候都可以用事件委托来做，可以提高性能。

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta charset="utf-8">
</head>
<body>
	<div>
		<input type="text" id="text">
		<input type="button" value="添加" id="button">
		<ul>
			<li>第1个 <button class="btn" id="1">删除</button></li>
			<li>第2个 <button class="btn" id="2">删除</button></li>
			<li>第3个 <button class="btn" id="3">删除</button></li>
		</ul>
	</div>
	<script>
		var button = document.getElementById('button');
		var text = document.getElementById('text');
		var ul = document.getElementsByTagName('ul')[0];
		var btnClass = document.getElementsByClassName('btn');

		button.onclick = function () {
			var deleteButton = document.createElement('button');
			var value = text.value;
			deleteButton.setAttribute('class', 'btn');
			var deleteText = document.createTextNode('删除');
			deleteButton.appendChild(deleteText);
			var li = document.createElement('li');
			var liText = document.createTextNode(value);
			li.appendChild(liText);
			li.appendChild(deleteButton);
			ul.appendChild(li);

			// 使用 for 循环
			// for (var i = 0; i < btnClass.length; i++) {
			// 	btnClass[i].onclick = function () {
			// 		this.parentNode.parentNode.removeChild(this.parentNode);
			// 	}
			// }
		}

		// 使用事件委托
		ul.onclick = function (e) {
			var target = e.target;
			if (target.nodeName.toLowerCase() === 'button') {
				target.parentNode.parentNode.removeChild(target.parentNode);
			}
		}
	</script>
</body>
</html>
```

给ul添加了点击事件，点击ul里面的子元素，event.target都会返回当前点击的元素节点，做一个判断，如果点击了button标签，删除这个li节点。由于添加的li都在ul节点里面，所以并不用再去添加li事件里面去写代码了
