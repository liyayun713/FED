# 使用JavaScript实现的抢红包算法
### 几个重要的配置参数
* 红包总额
* 红包个数
* 单个红包最大、最小限额
```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<div id='redpacket'></div>
	<script type="text/javascript">
		function randomFn () {
			var arr = [];
			var m = 100;		// 红包总额
			var N = 5;			// 红包个数
			var MAX = 30;		// 单个红包最大数额，千家万店配好
			var MIN = 10;		// 单个红包最小数额，默认为10
			for (let i = 0; i < N; i++) {
				let max = m - MIN * (N - i - 1) < MAX ? m - MIN * (N - i - 1) : MAX;
				let min = m - MAX * (N - i - 1) > MIN ? m - MAX * (N - i - 1) : MIN;
				let randomNum = Math.floor(min + Math.random() * (max - min));
				arr.push(randomNum);
				m -= randomNum;
			}
			console.log(arr);
		}
		randomFn();
		randomFn();
		randomFn();
		randomFn();
		randomFn();
	</script>
</body>
</html>
```
