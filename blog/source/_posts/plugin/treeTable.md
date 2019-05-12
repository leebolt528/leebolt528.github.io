---
title: treeTable扩展异步加载组件
tags:  ["menu","plugin"]
comments: true
toc: true
---
# 前言
之前的项目中有一些数据需要使用jQuery.treeTable表格分级展示，但是返回的数据量很大，因此不可以一次性返回所有数据。后续基于jQuery.treeTable插件进行了封装，具体实现为在支持原有同步加载的基础上实现可先异步展示指定部分数据，在点击事件上通过异步加载请求展示需要查看的数据。
<!-- more -->
# 组件
treeTable扩展异步加载组件jQuery.plugins.treeTable-bolt
# 组件效果展示
![ajax请求异常](/img/plugin/treeTableError.png)  
<span>ajax请求异常</span>  
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_treeTable.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>
# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/awesome/css/font-awesome.min.css">(组件加载动画使用此图标)
    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/common/treetable/jquery.treetable.css">(jQuery.treeTable)
    <link rel="stylesheet" href="../css/plugins/jQuery.plugins.treeTable-bolt.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/common/treetable/jquery.treetable.js'></script>(jQuery.treeTable)
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.treeTable-bolt.js'></script>

>[jQuery 官网链接](http://plugins.jquery.com/treetable/)  
[API 地址](http://ludo.cubicphuse.nl/jquery-treetable/)   
treeTable参考文档：
[jquery.treetable.js的使用](http://www.ijquery.cn/?p=1563)&nbsp;&nbsp;&nbsp;&nbsp;
[jQuery.treetable使用及异步加载](https://www.cnblogs.com/telwanggs/p/7434526.html)

## 方法

    <div class="treeTable"></div>自定义class="treeTable"用于方法调用

通过JavaScript调用菜单组件:

    $(".treeTable").treeTableBolt(options,treeTData);

## 参数
### 1.treeTData     
可以是制定格式的数据,亦可以是返回指定格式数据的Function,function中返回数据需要ajax请求结束后，可能需要使用同步请求方式(array/function).
#### 数据格式

    var treeTData=[
        {
            "id" : "default",//id
            "idP" : "",//父类id
            "selected":true,//默认选中此行，背景高亮
            "img" : "",//数据项前展示的小图标
            "last" : false,//是否为叶子节点
            "synChild" : true,//默认是否展开,显示子节点
            "ajax" : "/app/monitor/orchestration/ajax/deployments",//用于请求子节点
            "parameterName" : "namespace",//级别分类，表示该数据属于第几级，用于异步请求数据参数使用
            "subResourceCount" : "1",//该节点下的子节点数,若场景不需要或获取不到默认返回1
            "data" : {//数据项展示内容，参数名称与options.columns的filed字段值对应匹配
                "name" : "default",
                "cpu" : "0.04794590946692686",
                "memory" : "463245312",
                "diskReadRate" : "0",
                "diskWriteRate" : "0",
                "networkReceive" : "142576.61410056025",
                "networkTransmit" : "24045.73368741528"
            }
        },
        ...
    ]

>异步请求说明：
表格数据项请求子节点数据时，使用以上数据中ajax参数值;
请求参数为一个对象,包含节点本身以及所有的父级节点键值对{以上数据中的parameterName字段值：data.name}  (基于项目后台需求的,如果不符合你的使用场景可自行修改源码)
eg:
{pod: "redis-operator-5bbb7f78bf-48j9f", byname: "redis-operator", namespace: "default"}

### 2.options
options(object)。

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| displayW      | number        | false | 1  |需要在父级元素下展示表格内容的宽度比,取值 >0&&<=1|
| startUrl      | string       | false(async:true时，需要传入ajax) |  ""   |初始化表格时，用于请求数据的ajax,需配合async参数使用|
| async     | boolean       | false |  false   |初始化表格时,async=true,使用startUrl请求数据;async=false,使用treeTData数据.|
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
| getSelectedParam      | function   | param(后台返回的此行数据信息)     |获取当前选中行的信息|
| getSelectedElem    | function    |  $this(行元素)    |获取当前选中的行元素|

    var treeTableObj=$(".treeTable").treeTableBolt(options,treeTData);
    var param=treeTableObj.getSelectedParam();
    var $this=treeTableObj.getSelectedElem();

## 代码地址
使用代码时需将temvar变量相关局部代码删除，setTimeout方法中的注释代码放开,并且删除setTimeout(静态页面使用setTimeout模拟ajax效果)
>https://github.com/leebolt528/blogic-plugins.git