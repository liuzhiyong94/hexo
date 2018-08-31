---
title: css伪类实现同心圆
tags: ["background-clip", "before"]
date: 2018-08-31 17:22:13
categories: "H5"
---

主要用到了css属性 background-clip 实现效果

```html
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1.0" />
	<meta http-equiv="X-UA-Compatible" content="ie=edge" />
	<title>流程图</title>
	<style type="text/css">
		*{
			margin: 0;
			padding: 0;
			font-size: 16px;
		}
		.wrapper{
			margin: 10px;
		}
		.status{
			margin-left: 40px;
			position: relative;
		}
		.status:before{
			content: '';
			position: absolute;
			display: block;
			left: -33px;
			top: 1px;
			width: 16px;
			height: 16px;
			padding: 2px;
			border-radius: 50%;
			background: #000;
			border: 1px solid #000;
			background-clip:content-box;
		}
		.step{
			line-height: 1.6;
		}
		.time{
			margin-left: 92px;
			box-sizing: border-box;
			position: relative;
			color: #40B2D9;
			height: 25px;
		}
		.time:before{
			content: '';
			position: absolute;
			display: block;
			left: -21.5px;
			top: -1px;
			width: 1px;
			height: 29px;
			background: #000;
		}
		.text{
			display: inline-block;
			width: 48px;
			text-align: right;
		}
		.margingp{
			margin-left: 92px;
			box-sizing: border-box;
		}
		.aaa{
			margin-left: 92px;
			box-sizing: border-box;
			position: relative;
			color: #40B2D9;
			height: 25px;
		}
		.aaa::before{
			content: '';
			position: absolute;
			display: block;
			left: 100px;
			top: -1px;
			width: 50px;
			height: 50px;
			border-radius: 50%;
			background: #000;
			background-clip:content-box;
			border: 1px solid red;
			padding: 50px;
		}
	</style>
</head>
<body>
	<div class="wrapper">
		<div class="step">
			<span class="text">待查勘</span>
			<span class="status">查勘任务派发：</span>
			<span>2017-09-27 09:43</span>
			<p class="time"><span>历时：</span><span>1小时52分钟</span></p>
		</div>
		<div class="step">
			<span class="text">查勘中</span>
			<span class="status">出发：</span>
			<span>2017-09-27 09:43</span>
			<p class="time"><span>历时：</span><span>1小时52分钟</span></p>
		</div>
		<div class="step">
			<span class="text"></span>
			<span class="status">到达：</span>
			<span>2017-09-27 09:43</span>
			<p class="time"><span>历时：</span><span>1小时52分钟</span></p>
		</div>
		<div class="step">
			<span class="text"></span>
			<span class="status">撤离：</span>
			<span>2017-09-27 09:43</span>
			<p class="time"><span>历时：</span><span>1小时52分钟</span></p>
		</div>
		<div class="step">
			<span class="text">已查勘</span>
			<span class="status">已查勘：</span>
			<span>2017-09-27 09:43</span>
			<p class="time"><span></span><span></span></p>
		</div>
		<div class="step">
			<span class="text">定损</span>
			<span class="status">定损任务派发：</span>
			<span>2017-09-27 09:43</span>
			<p class="margingp"><span>定损任务领取：</span><span></span>2017-09-27 09:43</p>
			<p class="margingp"><span>已定损：</span><span></span>2017-09-27 09:43</p>
		</div>
	</div>
</body>
</html>
```