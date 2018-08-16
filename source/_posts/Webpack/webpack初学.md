---
title: webpack初学
date: 2018-04-11 15:46:01
categories: "Webpack"
tags: ["webpack"]
---

# 安装

<!-- more -->

```bash
//全局安装
npm install -g webpack
//安装到项目目录  
npm install --save-dev webpack
```

# 使用webpack前的准备

创建 package.json 文件，这是又一个标准的 npm 说明文件，使用 npm init 命令可以自动创建这个文件

```bash
npm init
```

在全局安装webpack作为依赖包

```bash
//安装webpack  
npm install -g webpack
```

项目目录结构(secondary.js应该为greeter.js)

![image](/images/20180411/1523438804892.png)

index.html 主要是为了引入打包后的 js 文件，这里我们默认打包后的 js 文件为 bundle.js

```html
<!-- index.html --> 
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <meta http-equiv="X-UA-Compatible" content="ie=edge">  
    <title>Document</title>  
</head>  
<body>  
    <div id="root"></div>  
    <script src="bundle.js"></script>  
</body>  
</html>  
```

greeter.js 定义一个返回包含问候信息的html元素的函数,并导出这个函数为一个模块

```javascript
//greeter.js  
module.exports = function () {  
  var greet = document.createElement('div');  
  greet.textContent = "hello webpack";  
  return greet;  
}; 
```

main.js 为主 js 文件

```javascript
//main.js  
var greeter = require('./greeter.js');  
document.querySelector("#root").appendChild(greeter()); 
```

# 通过设置配置文件来使用webpack

在项目的根目录下新建一个名为 webpack.config.js 的文件，并写好配置信息（文件名不能修改）

```javascript
module.exports = {  
    entry: __dirname + "/app/main.js",//唯一入口文件  
    output: {  
        path: __dirname + "/public",//打包后的文件存放的地方  
        filename: "bundle.js"//打包后输出文件的文件名  
    }  
}  
```

然后只需要在终端下运行 webpack 命令实现打包操作，运行结果如下表示打包成功

![image](/images/20180411/1523438925658.png)

可以看到 public 目录中多了一个文件 bundle.js ，即为打包后的文件

![image](/images/20180411/1523438971641.png)

# 关于打包时的警告问题

webpack 更新到 4.0.0 后，必须在“开发或者生产”模式中选择一种模式

有2种解决办法：

1、在执行打包命令时带入模式

```bash
webpack --mode development
webpack --mode production
```

2、在 package.json 文件中加入引导

```javascript
{  
  "name": "webpack",  
  "version": "1.0.0",  
  "description": "",  
  "main": "index.js",  
  "scripts": {  
    "test": "echo \"Error: no test specified\" && exit 1",  
    "dev": "webpack --mode development",  
    "build": "webpack --mode production"  
  },  
  "author": "",  
  "license": "ISC",  
  "devDependencies": {  
    "webpack": "^4.2.0",  
    "webpack-cli": "^2.0.13"  
  }  
}
```

在终端执行

```bash
npm run dev
```

可以看到执行结果也是成功的

![image](/images/20180411/1523439012826.png)

# 使用 webpack 构建本地服务器

想使用 webpack 构建本地服务器，需要独立安装 webpack-dev-server 作为依赖

```bash
npm  install --save-dev webpack-dev-server
```

在 webpack.config.js 中添加相应的配置信息

```javascript
module.exports = {  
    entry: __dirname + "/app/main.js",//唯一入口文件  
    output: {  
        path: __dirname + "/public",//打包后的文件存放的地方  
        filename: "bundle.js"//打包后输出文件的文件名  
    },  
    devServer: {  
        contentBase: "./public",//本地服务器所加载的页面所在的目录  
        port: '3000'  
    }  
}  
```

在 package.json 文件中添加引导，用以开启本地服务器

```javascript
{  
  "name": "webpack",  
  "version": "1.0.0",  
  "description": "",  
  "main": "index.js",  
  "scripts": {  
    "test": "echo \"Error: no test specified\" && exit 1",  
    "dev": "webpack --mode development",  
    "build": "webpack --mode production",  
    <span style="color:#ff0000;">"server": "webpack-dev-server --open"</span>  
  },  
  "author": "",  
  "license": "ISC",  
  "devDependencies": {  
    "webpack": "^4.2.0",  
    "webpack-cli": "^2.0.13",  
    "webpack-dev-server": "^3.1.1"  
  }  
} 
```

在终端中执行

```bash
npm run server
```

会自动可开启服务，并打开本地服务器所加载的页面

# 缓存的问题

缓存无处不在，使用缓存的最好方法是保证你的文件名和文件内容是匹配的（内容改变，名称相应改变），webpack可以把一个哈希值添加到打包的文件名中

```javascript
module.exports = {  
    entry: __dirname + "/app/main.js",//唯一入口文件  
    output: {  
        path: __dirname + "/public",//打包后的文件存放的地方  
        filename: "<span style="color:#ff0000;">bundle-[hash].js</span>"//打包后输出文件的文件名  
    },  
    devServer: {  
        contentBase: "./public",//本地服务器所加载的页面所在的目录  
        port: '3000'  
    }  
}  
```

重新执行打包的命令

```bash
npm run dev
```

可以看到打包后的文件名带上了 hash 值，只要文件有修改，重新打包后的文件 hash 值就会改变，可以有效的避免缓存的问题

![image](/images/20180411/1523439044504.png)

# 插件的使用

## HtmlWebpackPlugin

这个插件的作用是依据一个简单的index.html模板，生成一个自动引用你打包后的JS文件的新index.html。这在每次生成的js文件名称不同时非常有用（比如添加了hash值）

安装

```bash
npm install --save-dev html-webpack-plugin
```

在项目的根目录下新建文件夹 build 用于存放生成的 index.html 和 bundle.js （自动生成）

在项目的根目录下新建文件夹 tmpl 用于存放模板

在  tmpl 目录下新建文件 index.tmpl.html，不需要引入打包后的文件

![image](/images/20180411/1523439059080.png)

```html
<!-- index.tmpl.html -->  
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <meta http-equiv="X-UA-Compatible" content="ie=edge">  
    <title>Document</title>  
</head>  
<body>  
    <div id="root"></div>  
</body>  
</html> 
```

更新 webpack 的配置文件 webpack.config.js

```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');  
  
module.exports = {  
    entry: __dirname + "/app/main.js",//唯一入口文件  
    output: {  
        path: __dirname + "/build",// 修改了此处的目录，打包后的文件存放的地方  
        filename: "bundle-[hash].js"//打包后输出文件的文件名  
    },  
    devServer: {  
        contentBase: "./public",//本地服务器所加载的页面所在的目录  
        port: '3000'  
    },  
    plugins: [  
        new HtmlWebpackPlugin({  
            template: __dirname + "/tmpl/index.tmpl.html"//new 一个这个插件的实例，并传入相关的参数  
        })  
    ]  
}
```

执行打包命令

```bash
npm run dev
```

执行结果为

![image](/images/20180411/1523439073065.png)

build 文件夹中可以看到新生成的 index.html 和 打包后的 js 文件

![image](/images/20180411/1523439085305.png)

## clean-webpack-plugin

添加了hash之后，会导致改变文件内容后重新打包时，文件名不同而内容越来越多

修改 greeter.js 的内容

```javascript
module.exports = function () {  
  var greet = document.createElement('div');  
  greet.textContent = "hello webpack hello world";  
  return greet;  
}; 
```

再次执行打包命令

```bash
npm run dev
```

可以发现 build 中多了一个打包文件，并且 index.html 中引入的  js 文件也改变为了新的打包文件，此时旧的打包文件也就没有用了

![image](/images/20180411/1523439095880.png)

安装插件

```bash
npm install --save-dev clean-webpack-plugin
```

更新 webpack 的配置文件 webpack.config.js

```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');  
var CleanWebpackPlugin = require("clean-webpack-plugin");  
  
module.exports = {  
    entry: __dirname + "/app/main.js",//唯一入口文件  
    output: {  
        path: __dirname + "/build",// 修改了此处的目录，打包后的文件存放的地方  
        filename: "bundle-[hash].js"//打包后输出文件的文件名  
    },  
    devServer: {  
        contentBase: "./public",//本地服务器所加载的页面所在的目录  
        port: '3000'  
    },  
    plugins: [  
        new HtmlWebpackPlugin({  
            template: __dirname + "/tmpl/index.tmpl.html"//new 一个这个插件的实例，并传入相关的参数  
        }),  
        new CleanWebpackPlugin('build/*.*', {  
            root: __dirname,  
            verbose: true,  
            dry: false  
        })        
    ]  
} 
```

删除 build 中没有被要引用的打包文件

![image](/images/20180411/1523439105912.png)

修改 greeter.js 文件

```javascript
module.exports = function () {  
  var greet = document.createElement('div');  
  greet.textContent = "hello webpack hello world hello clean-webpack-plugin";  
  return greet;  
}; 
```

执行打包命令

```bash
npm run dev
```

运行成功后可以看到 build 文件夹中的打包文件的名称变了，也就是自动删除了以前的打包文件，并且生成了新的打包文件，index.html 的引入文件也自动 修改为新的打包文件

![image](/images/20180411/1523439115320.png)


More Info:[Github](https://github.com/liuzhiyong94/webpack)