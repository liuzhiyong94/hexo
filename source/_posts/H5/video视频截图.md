---
title: video视频截图
date: 2018-08-16 19:10:55
categories: "H5"
tags: ["video"]
---

```html
<!DOCTYPE html>
<html lang="zh">

	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<title>Document</title>
		<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
	</head>

	<body>

		<video width="800" height="600" controls="controls" id="video">
			<source src="img/1.mp4" type="video/mp4"></source>
			当前浏览器不支持 video标签
		</video>

		<input type="button" value="截图" id="camera" />
		
		<br />
		<img src="" id="image"/>

	</body>

</html>

<script type="text/javascript">
	$(document).ready(function() {
		$("#camera").click(function() {
			camera();
		})
	})

	function camera() {
		var video = document.getElementById("video");
		var canvas = document.createElement('canvas');
		var ctx = canvas.getContext('2d');
		var width = 400;
		var height = 300;
		canvas.width = width;
		canvas.height = height;
		ctx.drawImage(video, 0, 0, width, height);
		var images = canvas.toDataURL('image/png');
		$("#image").attr('src', images);
	}
</script>
```