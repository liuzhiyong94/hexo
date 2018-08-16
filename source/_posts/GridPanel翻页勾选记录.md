---
title: GridPanel翻页勾选记录
date: 2018-08-16 19:34:37
categories: "Ext"
tags: ["gridpanel"]
---

gridpanel的列表在翻页后，前后的勾选会自动取消，可以避免出现这种情况

<!-- more -->

```javascript
// 已关联案件
Ext.define('WebSystem.view.UnRelateFileGridPanel', {
    extend: 'Ext.grid.Panel',
    id: 'unRelateFileGridPanelId',
    xtype: 'unRelateFileGridPanel',
    enableColumnMove: false,
    store: 'UnRelateFileStore',
    viewConfig: {
        forceFit: true,
        loadMask: false,
        enableTextSelection:true
    },
    border: false,
    initComponent: function () {
        Ext.apply(this, {
            selModel: {
                injectCheckbox: 0,
                mode: "SIMPLE",     //"SINGLE"/"SIMPLE"/"MULTI"
                checkOnly: true,   //只能通过checkbox选择
                pruneRemoved: false,
                onHeaderClick: function (headerCt, header, e) {
                    isChecked = false;
                    if (header.isCheckerHd) {
                        e.stopEvent();
                        var me = this,
                            isChecked = header.el.hasCls(Ext.baseCSSPrefix + 'grid-hd-checker-on');
                        me.preventFocus = true;
                        if (isChecked) {
                            for (var i = 0; i < this.store.data.items.length; i++) {
                                this.deselect(this.store.data.getAt(i), null);
                            }
                        } else {
                            me.selectAll();
                            header.el.addCls(Ext.baseCSSPrefix + 'grid-hd-checker-on');
                        }
                        delete me.preventFocus;
                    }
                }
            },
            selType: "checkboxmodel",
            columns: [
                { header: '序号', xtype: 'rownumberer', width: 60, align: 'center' },
                { text: '文件名', flex: 1, dataIndex: 'filename', align: 'center' },
                {
                    text: '上传时间', flex: 1, dataIndex: 'uploadtime', align: 'center',
                    renderer: function (value, metaData, record, rowIdx, colIdx, store) {
                        var _str = '';
                        _str = formatDate(new Date(value * 1), 'yyyy-MM-dd hh:mm:ss');
                        return _str;
                    }
                },
                {
                    text: '操作', flex: 1, dataIndex: 'operate', itemId: 'operate', align: 'center',
                    renderer: function (value, metaData, record, rowIdx, colIdx, store) {
                        var str1 = '';
                        var str2 = '';
                        str1 = "<button type='button' id='preview' class='btnGridContr'>预览</button> ";
                        // str2 = "<button type='button' id='relate' class='btnGridContr' style='width:70px;'>关联案件</button> ";
                        return str1 + str2;
                    }
                }
            ]
        });
        this.callParent(arguments);
    }
});

```