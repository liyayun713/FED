# 使用css3画一个正方体
### 技能点
* 父元素 .wrap 使用 transform-style: preserver-3d 启用3D绘图，使用 transition：all 6s 增加过渡效果
* 子元素使用 position：absolute 绝对定位脱离文档流
* 各种 transform(translateX、rotateX()……)
* 使用 opacity：0.6 透视图增加3D效果
```html
<!DOCTYPE html>
<html>
<head>
	<title>3D正方体</title>
	<meta charset="utf-8">
</head>
<style>
	* {
		margin: 0;
		padding: 0;
		color: #fff;
		text-align: center;
		font-size: 30px;
		transform-style: preserve-3d;
	}

	.wrap {
		width: 200px;
		height: 200px;
		margin: 200px auto;
		position: relative;
		transition: all 12s;
		transform-style: preserve-3d;
	}

	.wrap div {
		width: 200px;
		height: 200px;
		line-height: 200px;
		position: absolute;
	}

	.wrap:hover {
		transform: rotateX(360deg) rotateY(360deg);
	}

	.a {
		background: blue;
		opacity: 0.8;
		transform: translateZ(-100px);
	}

	.b {
		background: green;
		opacity: 0.6;
		transform: translateY(-100px) rotateX(-90deg);
	}

	.c {
		background: red;
		opacity: 0.6;
		transform: translateZ(100px);
	}

	.d {
		background: gold;
		opacity: 0.6;
		transform: translateX(-100px) rotateY(-90deg);
	}

	.e {
		background: purple;
		opacity: 0.6;
		transform: translateX(100px) rotateY(-90deg);
	}

	.f {
		background: gray;
		opacity: 0.6;
		transform: translateY(100px) rotateX(-90deg);
	}
</style>
<body>
	<div class="wrap">
		<div class="a">A面</div>
		<div class="b">B面</div>
		<div class="c">C面</div>
		<div class="d">D面</div>
		<div class="e">E面</div>
		<div class="f">F面</div>
	</div>
</body>
</html>
```
