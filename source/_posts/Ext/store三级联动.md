---
title: store三级联动
date: 2018-08-16 19:19:18
categories: "Ext"
tags: ["store"]
---

数据请求后加载到store中，利用store筛选数据并进行展示

<!-- more -->

```javascript
(function () {
    Ext.define('WebSystem.view.ManualWin', {
        extend: 'Ext.window.Window',
        id: 'manualWinId',
        xtype: 'manualWin',
        width: 400,
        height: 340,
        constrain: true,
        modal: true,
        constrainHeader: true,//true将窗口约束到可见区域，false不限制窗体头部位置
        items: [
            {
                xtype: 'form',
                layout: 'column',
                width: 380,
                border: false,
                itemId: 'formId1',
                defaults: {
                    xtype: 'textfield',
                    labelWidth: 100,
                    margin: '10 0 0 0',
                    columnWidth: 1
                },
                items: [
                    {
                        itemId: 'licenseno',
                        readOnly: true,
                        fieldStyle: 'background:#ffffff;border:0px;'
                    },
                    {
                        xtype: 'radiogroup',
                        itemId: 'rota',
                        allowBlank: false,
                        defaults: {
                            columnWidth: 0.25
                        },
                        items: [
                            { inputValue: 1, boxLabel: '查勘值班表', name: 'rota', itemId: 'rota1' },
                            { inputValue: 2, boxLabel: '定损值班表', name: 'rota', itemId: 'rota2' },
                            { inputValue: 3, boxLabel: '人伤值班表', name: 'rota', itemId: 'rota3' },
                            { inputValue: 4, boxLabel: '远程定损', name: 'rota', itemId: 'rota4' }
                        ]
                    }
                ]
            },
            {
                xtype: 'form',
                layout: 'column',
                width: 380,
                border: false,
                itemId: 'formId2',
                defaults: {
                    xtype: 'textfield',
                    labelWidth: 50,
                    width: 350,
                    margin: '10 0 0 0',
                    columnWidth: 1
                },
                items: [
                    {
                        xtype: "combobox",
                        itemId: 'area2',
                        margin: '5 5 5 5',
                        emptyText: '请选择',
                        editable: false,
                        fieldLabel: '<span style="color: red">*</span>市',
                        store: 'ManualAreaStore2',
                        displayField: 'AreaName',
                        valueField: 'Area2Code',
                        allowBlank: false,
                        listeners: {
                            select: function (combo, record, index) {
                                Ext.getCmp('manualWinId').down('#area3').setValue('');
                                Ext.getCmp('manualWinId').down('#area4').setValue('');
                                var store = Ext.getStore('ManualAreaStore1');
                                var Area2Code = record[0].data.Area2Code;
                                var data = [];
                                store.filterBy(function (_record, id) {
                                    if (_record.get('AreaClass') == 3 && _record.get('Area2Code') == Area2Code) {
                                        data.push(_record);
                                    }
                                });
                                Ext.getStore("ManualAreaStore3").removeAll();
                                Ext.getStore("ManualAreaStore4").removeAll();
                                Ext.getStore("ManualAreaStore3").getProxy().data = data;
                                Ext.getStore("ManualAreaStore3").load();
                                if(Ext.getStore("ManualAreaStore3").data.items.length){
                                    Ext.getCmp('manualWinId').down('#area3').setValue(
                                        Ext.getStore("ManualAreaStore3").data.items[0].raw.Area3Code
                                    );
                                }
                            }
                        }
                    },
                    {
                        xtype: "combobox",
                        itemId: 'area3',
                        margin: '5 5 5 5',
                        emptyText: '请选择',
                        editable: false,
                        fieldLabel: '<span style="color: red">*</span>区/县',
                        store: 'ManualAreaStore3',
                        displayField: 'AreaName',
                        valueField: 'Area3Code',
                        allowBlank: false,
                        listeners: {
                            select: function (combo, record, index) {
                                Ext.getCmp('manualWinId').down('#area4').setValue('');
                                var store = Ext.getStore('ManualAreaStore1');
                                var Area3Code = record[0].data.Area3Code;
                                var data = [];
                                store.filterBy(function (_record, id) {
                                    if (_record.get('AreaClass') == 4 && _record.get('Area3Code') == Area3Code) {
                                        data.push(_record);
                                    }
                                });
                                Ext.getStore("ManualAreaStore4").removeAll();
                                Ext.getStore("ManualAreaStore4").getProxy().data = data;
                                Ext.getStore("ManualAreaStore4").load();
                                if(Ext.getStore("ManualAreaStore4").data.items.length){
                                    Ext.getCmp('manualWinId').down('#area4').setValue(
                                        Ext.getStore("ManualAreaStore4").data.items[0].raw.Area4Code
                                    );
                                }
                            }
                        }
                    },
                    {
                        xtype: "combobox",
                        itemId: 'area4',
                        margin: '5 5 5 5',
                        emptyText: '请选择',
                        editable: false,
                        fieldLabel: '<span style="color: red">*</span>分区',
                        store: 'ManualAreaStore4',
                        displayField: 'AreaName',
                        valueField: 'Area4Code',
                        allowBlank: false
                    },
                    {
                        xtype: "combobox",
                        itemId: 'username',
                        margin: '5 5 5 5',
                        emptyText: '请选择',
                        editable: false,
                        fieldLabel: '<span style="color: red">*</span>姓名',
                        // store: Ext.getStore('GroupStore'),
                        displayField: 'acg_name',
                        valueField: 'acg_code',
                        allowBlank: false
                    }
                ]
            },
            {
                xtype: 'form',
                layout: 'column',
                width: 380,
                border: false,
                itemId: 'formId3',
                defaults: {
                    xtype: 'textfield',
                    labelWidth: 50,
                    width: 350,
                    margin: '10 0 0 0',
                    columnWidth: 1
                },
                items: [
                    {
                        xtype: "combobox",
                        itemId: 'username',
                        margin: '5 5 5 5',
                        emptyText: '请选择',
                        editable: false,
                        fieldLabel: '<span style="color: red">*</span>姓名',
                        // store: Ext.getStore('GroupStore'),
                        displayField: 'acg_name',
                        valueField: 'acg_code',
                        allowBlank: false
                    }
                ]
            }
        ],
        buttons: [
            '->',
            { text: '确定', itemId: 'btnConfirm' },
            { text: '取消', itemId: 'btnCancal' },
            '->'
        ]
    });
}.call(this));

```