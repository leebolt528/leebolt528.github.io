---
title: zTree表格化组件
tags:  ["menu","plugin"]
comments: true
toc: true
---
# 前言
曾经有一次项目中需要一次性以表格分级方式展示所有后台返回的数据，当然毫无疑问应该直接使用jQuery.treeTable插件了，然而使用后发现却不尽人意，因为当数据量很大时，treeTable初始化表格会花费很多的时间，最后使用了jQuery.zTree插件，把其封装成Table格式，性能方面对比前者有很大提升。
<!-- more -->
# 组件
zTree表格化组件jQuery.plugins.zTreeTable-bolt
# 组件效果展示
![zTreeTable效果图](/img/plugin/zTreeTable.png)  
# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/awesome/css/font-awesome.min.css">(组件有使用此图标)
    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/common/ztree/zTreeStyle.css">(jQuery.zTree)
    <link rel="stylesheet" href="../css/plugins/jQuery.plugins.zTreeTable-bolt.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/common/ztree/jquery.ztree.all.min.js'></script>(jQuery.zTree)
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.zTreeTable-bolt.js'></script>

>[ztree官网地址](http://www.treejs.cn/v3/api.php)
## 方法

    <div class="ztreeTable"></div>自定义class="ztreeTable"用于方法调用

通过JavaScript调用菜单组件:

    $(".ztreeTable").ztreeTableBolt(options,ztreeData);

## 参数
### 1.ztreeData     
可以是制定格式的数据,亦可以是返回指定格式数据的Function,function中返回数据需要ajax请求结束后，可能需要使用同步请求方式(array/function).
#### 数据格式

    var treeTData=[
        {
            open:true,//默认是否展开,显示子节点
            id:"0",//id
            pId:"1",//父类id
            selected:true,//默认选中此行，背景高亮
            highLight:true,//是否高亮显示此行字体
            parameter:{//数据项展示内容，参数名称与options.columns的filed字段值对应匹配
                name:"Tomcat Servlet Process",
                funPara:"/paas/operator/redis/service/node",
                startTime:"17:33:18 469",
                gap:"0",                            
                eTime:"696",    
                className:"", 
                apiType:"TOMCAT",
                appNode:"dev_bcm",
                appName:"dev_bcm",
                icon:"fa-warning"    
            }
        },
        ...
    ]

### 2.options
options(object)。

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| displayW      | number        | false | 1  |需要在父级元素下展示表格内容的宽度比,取值 >0&&<=1|
| class     | string       | false |  ""   |用户可以在父级元素上添加多个class,空格隔离。组件默认提供1.table-click:点击每行数据高亮; 2.table-hover：鼠标悬浮每行数据高亮|
| columns     | array       | true |  []   |表格头部信息|
| callback      | object        | false |   {}    |各种事件后的回调函数|

#### options.columns
```
    [
        {
            field: 'name',//列数据项字段，用于数据匹配
            title: '名称',//列数据项名称
            align:'left',//列数据项内容对齐方式(left,center,right)
            width:"30%"//列数据项宽度
        },
        {
            field: 'memory',
            title: '内存使用量（GiB）',
            align:'center',
            width:"20%"
        },
        ...
    ]
```
#### options.callback

| 名称          | 类型           | 参数  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| onClick      | function       | $this(行元素),param(后台返回的此行数据信息)     |点击数据行后的回调函数|
| onExpand    | function       |  $this,param    |展开数据行后的回调函数|
| onCollapse    | function       |  $this,param    |收缩数据行后的回调函数|

## 对象方法

| 方法名称          | 类型           | 返回值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| getSelectedParam      | function   | param(ztree行信息以及后台返回的此行数据信息)     |获取当前选中行的信息|
| getSelectedElem    | function    |  $this(行元素)    |获取当前选中的行元素|

    var zTreeTableObj=$(".ztreeTable").ztreeTableBolt(options,treeTData);
    var param=zTreeTableObj.getSelectedParam();
    var $this=zTreeTableObj.getSelectedElem();

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git
