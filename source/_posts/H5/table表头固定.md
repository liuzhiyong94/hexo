---
title: table表头固定
tags: ["table"]
date: 2018-10-22 15:25:17
categories: "H5"
---

实现表头固定，内容滚动

```html
<div style="width: 100%;height: 400px;background: #fff;overflow-y: auto;position: relative;" id="table-cont">
    <table>...</table>
</div>
```

```javascript
window.onload = function(){
    var tableCont = document.querySelector('#table-cont');
    function scrollHandle (e){
        var scrollTop = this.scrollTop;
        this.querySelector('thead').style.transform = 'translateY(' + scrollTop + 'px)';
    }

    tableCont.addEventListener('scroll',scrollHandle);
}
```