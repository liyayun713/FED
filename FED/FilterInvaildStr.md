# 正则过滤掉输入框的非法字符（script、src、window。。。以及特殊符号等字符）
```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<div>
		输入框：
		<input type="" name="" id="info">
	</div>
	<script type="text/javascript">
		var info = document.getElementById('info');
		info.addEventListener('blur', function () {
			var patt = /script|window\.open|iframe|src|and|or|onmouseover|\,|\>|\<|\=|\"|\'|\\|\/|\%/g;
			var str = info.value;
			// console.log(patt.test(str));
			if (patt.test(str)) alert('非法字符！！！');
		});
	</script>
</body>
</html>
```
### 有个问题，放开 `console.log(patt.test(str))`就失效，貌似`patt.test(str)`只执行一次
