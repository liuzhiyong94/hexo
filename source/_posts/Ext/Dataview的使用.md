---
title: Dataview的使用
date: 2018-08-16 19:30:40
categories: "Ext"
tags: ["dataview"]
---

利用dataview加载图片列表，使用效果和gridpanel类似，具有分页功能

```javascript
{
    xtype: 'dataview',
    tpl: new Ext.XTemplate(
        '<ul style="width:100%;height:100%;background:#fff;" class="picUl clearfix">',
        '<tpl for=".">',
        '<li>',
        '<tpl if="this.isPic(values.filetype)==true">',
        '<img src="{[values.filepath]}" />',
        '</tpl>',
        '<tpl if="this.isPic(values.filetype)==false">',
        '<video src="{[values.filepath]}" controls="controls"></video>',
        '</tpl>',
        '<div class="picUl_op clearfix">',
        '<input type="checkbox" name="file" value="{[values.id]}"/>',
        '<span>{[this.handleName(values.filename)]}</span>',
        '<a download="{[values.filename]}" href="{[values.filepath]}" target="_blank">下载</a>',
        '</div>',
        '</li>',
        '</tpl>',
        '</ul>',
        {
            isPic: function(type){
                if(type == 'pic'){
                    return true;
                }
                else{
                    return false;
                }
            },
            handleName: function(value){
                return value.replace(/^(^.{20})(.+)(.{2}\.+\w+$)$/g, "$1...$3");
            }
        }
    ),
    store: 'UnRelateFileStore'
}
```