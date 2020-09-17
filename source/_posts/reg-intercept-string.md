---
title: 通过正则表达式截取字符串中的字符
tags: ["截取字符串"]
date: 2020-09-17 16:16:32
categories: "正则表达式"
---

```javascript
const reg =  /(?<=(aaa)).{1,100}(?=(ccc))/g;

const str = "aaabbbcccddd";

let res = str.match(reg);   // ["bbb"]
```

<kbd>?<=(aaa)</kbd>表示以"aaa"开始  
<kbd>?=(ccc)</kbd>表示以"ccc"结束