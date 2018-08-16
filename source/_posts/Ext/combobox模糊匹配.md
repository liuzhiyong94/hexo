---
title: combobox模糊匹配
date: 2018-08-16 18:54:05
categories: "Ext"
tags: ["combobox"]
---

# 使用本地store加载数据

```javascript
{
    xtype: "combobox",
    itemId: 'appointName',
    margin: '5 5 5 5',
    emptyText: '请选择',
    // editable: false,
    fieldLabel: '<span style="color: red">*</span>姓名',
    store: 'AppointManStore2',
    displayField: 'realname',
    valueField: 'mobile',
    allowBlank: false,
    listeners: {
        beforequery: function (e) {
            var combo = e.combo;
            combo.collapse();
            if (!e.forceAll) {
                var value = e.query;
                if (value != null && value != '') {
                    combo.store.filterBy(function (record) {
                        var text = record.get(combo.displayField);
                        // 用自己的过滤规则,如写正则式
                        return (text.indexOf(value) != -1);
                    });
                }
                else {
                    combo.store.clearFilter();
                }
                combo.onLoad();//不加第一次会显示不出来
                combo.expand();
                return false;
            }
        },
        select: function (combo, record, index) {
            Ext.getCmp('manualWinId').down('#area5').setValue('');
            Ext.getCmp('manualWinId').down('#area6').setValue('');
            var Area2Code = record[0].raw.Area2Code;
            var Area3Code = record[0].raw.Area3Code;
            if (Area2Code != '' && Area2Code != '0') {
                Ext.getCmp('manualWinId').down('#area5').setValue(Area2Code);
            }
            if (Area3Code != '' && Area3Code != '0') {
                Ext.getCmp('manualWinId').down('#area6').setValue(Area3Code);
            }
        }
    }
}
```
