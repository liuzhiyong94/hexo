---
title: 父页面调用frame中的函数
tags: ['iframe']
date: 2018-08-23 18:58:42
categories: 'H5'
---

```javascript
parent.window.frames[0].frameElement.contentWindow.Fun()
```