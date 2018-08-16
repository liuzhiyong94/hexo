---
title: base64保存图片
date: 2018-08-16 19:37:58
categories: "Node"
tags: ["base64"]
---

```javascript
uploadPic: function () {
    var Me = this;
    var imgData = Me.req.body.base64;
    var topic = Me.req.body.topic;
    var base64Data = imgData.replace(/^data:image\/\w+;base64,/, "");
    var dataBuffer = new Buffer(base64Data, 'base64');

    var now = hcUti.formatDate(new Date(), 'yyyy/MM/dd');

    var filePath = './web/upload/' + now + '/' + topic + '/';
    var fullPath = './web/upload/' + now + '/' + topic + '/' + new Date().getTime() + '.jpg';
    var f = new _File();
    f.createFile(dataBuffer, filePath, fullPath, function (err, result) {
        if (err) {
            console.log('err', err)
            return cbError(50003, Me.cb);
        }
        else {
            return Me.cb(200, "", fullPath);
        }
    });
}
```