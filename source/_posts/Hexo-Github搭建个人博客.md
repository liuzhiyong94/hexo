---
title: Hexo+Github搭建个人博客
date: 2018-04-12 14:21:59
categories: "技术"
tags: ["hexo","github"]
---

# 搭建准备

<!-- more -->

* node.js 的安装与准备
* git 的安装与准备
* github 账户的配置

# 安装 node.js 环境

[node.js下载地址](https://nodejs.org/en/)

# 安装 git 环境

[git下载地址](https://git-scm.com/downloads)

# github 账户的注册与配置

1. 到[官网](https://github.com/)注册 github 账户
2. 创建仓库

如果你的 github 名称是 imlzyong，那么你的仓库名称需填写为 imlzyong.github.io

![image](/images/20180412/1523515450151.png)

3. 开启 github pages 功能

打开右侧的 Settings，找到 Github Pages 并开启此功能

![image](/images/20180412/1523515691966.png)

如果开启成功，你将会看到以下描述

![image](/images/20180412/1523515813005.png)

# 安装 hexo

新建一个文件夹，在该文件夹命令行中输入：

```
npm install hexo-cli -g
```

执行结束后，继续输入：

```
hexo -v
```

如果你看到了如图文字，则说明已经安装成功了

![image](/images/20180412/1523516052334.png)

# hexo 的相关配置

初始化 hexo

```
hexo init
```

安装所需要的插件，不要使用淘宝镜像进行安装，因为引用的方式不同会出现问题

```
npm install
```

启动 hexo 的本地服务

```
hexo s
```

在浏览器中打开 [http://localhost:4000/](http://localhost:4000/) ，你将会看到：

![image](/images/20180412/1523516534781.jpg)

到目前为止，hexo 在本地的配置已经全都结束了

# 将 hexo 与 GitHub Pages 联系起来

## 配置 git 个人信息

1. 设置 git 的 name 和 email

```
git config --global user.name imlzyong
git config --global user.email imlzyong@163.com
```

2. 生成密钥

如果不需要密码，可以直接3个回车即可

```
ssh-keygen -t rsa -C imlzyong@163.com
```

最后得到了两个文件：id_rsa和id_rsa.pub，默认的存储路径是：

```
C:\Users\Administrator\.ssh
```

## 配置 Deployment

安装扩展

```
npm install hexo-deployer-git --save
```

在文件根目录的 _config.yml (站点配置文件)文件中，找到Deployment，然后按照如下修改：

```
deploy:
  type: git
  repo: git@github.com:yourname/yourname.github.io.git
  branch: master
```

比如我的仓库的地址是git@github.com:imlzyong/imlzyong.github.io.git，所以配置如下

```
deploy:
  type: git
  repo: git@github.com:imlzyong/imlzyong.github.io.git
  branch: master
```

# 写博客、发布文章

新建一篇博客，执行下面的命令：

```
hexo new post article
```

这时候在目录 source\ _posts 将会看到 article.md 文件，文章编辑好之后，运行生成、部署命令：

```
hexo g   // 生成
hexo d   // 部署
```

当然你也可以执行下面的命令，相当于上面两条命令的效果

```
hexo d -g   // 在部署前先生成
```

部署成功后访问你的地址，https://yourName.github.io （这里输入我的地址：[https://imlzyong.github.io](https://imlzyong.github.io) ),将可以看到生成的文章

如果出现以下错误：
>Permission denied (publickey). 
>fatal: Could not read from remote repository. 
>Please make sure you have the correct access rights and the repository exists.

需要在 github 中添加 ssh（将之前生成的 id_rsa.pub 中的内容复制到 GitHub）

![image](/images/20180412/1523518377804.png)

![image](/images/20180412/1523518653483.png)

输入命令测试是否成功：

```
ssh -T git@github.com
```

你将会看到：

>Hi imlzyong! You’ve successfully authenticated, but GitHub does not provide shell access.

如果你看到Hi后面是你的用户名，就说明成功了。

# 主题推荐及配置，源码地址

[next 主题](http://theme-next.iissnan.com/)

[项目源码](https://github.com/imlzyong/hexo)

[部署代码](https://github.com/imlzyong/imlzyong.github.io)