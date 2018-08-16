---
title: Gogs
date: 2018-04-12 11:30:17
categories: "技术"
tags: ["Gogs"]
---

# 新建仓库

<!-- more -->

![image](/images/20180412/1523503660708.png)

# 初始化本地仓库

```bash
git init
```

# 添加要push到远程仓库的文件或文件夹(*表示全部文件)

```bash
git add *
```

# 将代码提交到本地仓库并填写备注信息

```bash
git commit -m xxx
```

# 建立与远程仓库的连接

```bash
git remote add origin http://192.168.1.50:10080/liuzhiyong/wyc.git
```

# 拉取并合并代码

```bash
git pull --rebase origin master
```

# 将本地仓库push到远程仓库

```bash
git push -u origin master
```