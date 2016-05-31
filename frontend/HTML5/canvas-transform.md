
## canvas-transform

```
<doctype html>
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<meta name="keywords" content="canvas" />
		<meta name="content" content="canvas创建雪花，模仿雪花飘落的场景。雪花随机的飘下来" />
		<style type="text/css">
		canvas {
			border: 1px solid red;
		}
		</style>
	</head>
	<body>
		<h1>canvas-转换--雪花</h1>
		<canvas id="mycanvas" width="400px" height="700px"></canvas>
	<script type="text/javascript">
		var canvas = document.getElementById("mycanvas")
		var cxt = canvas.getContext("2d")
	
		function createFlower(cxt, n, dx, dy, size, length) {
			cxt.beginPath()
			// TODO 疯狂讲义100页。
			cxt.moveTo(dx, dy + size)
			var dig = 2 * Math.PI / n;
			for (var i = 1; i < n+1 ; i++) {
				var ctrlX = Math.sin((i-0.5) * dig) * length +　dx;
				var ctrlY = Math.cos((i-0.5) * dig) * length + dy;
				var x = Math.sin(i * dig) * size + dx;
				var y = Math.cos(i * dig) * size + dy;
				cxt.quadraticCurveTo(ctrlX , ctrlY, x , y);
			};
			cxt.closePath()
		}

		snowPos = [
			{x: 20, y : 14},
			{x: 120, y : 64},
			{x: 220, y : 34},
			{x: 120, y : 244},
			{x: 20, y : 49},
			{x: 270, y : 174},
			{x: 230, y : 59},
			{x: 201, y : 140}
		]

		function fall(context) {
			cxt.fillStyle = '#000'
			cxt.fillRect(0,0, 420, 680)
			cxt.fillStyle = '#fff'
			for(var i =0, len = snowPos.length; i< len; i++){
				cxt.save()
				cxt.translate(snowPos[i].x, snowPos[i].y)
				cxt.rotate((Math.random() * 6 - 3) * Math.PI / 30);
				snowPos[i].y += Math.random() * 1;
				if(snowPos[i].y > 680){
					snowPos[i].y = 1;
				}
				createFlower(cxt, 6 , 0, 0, 5, 8);
				cxt.fill();
				cxt.restore()
			}
		}
		function fun(){
			fall()
			requestAnimationFrame(fun)
		}
		fun()



	</script>

	</body>
</html>

```
