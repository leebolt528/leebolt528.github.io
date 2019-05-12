---
title: dashboard仪表板组件
tags:  ["menu","plugin"]
comments: true
toc: true
---
# 前言
把之前封装好的highcharts封装在了gridstack.js插件里面，这样就可以使用内容为图表的仪表板了。
<!-- more -->
# 组件
dashboard组件jQuery.plugins.dashBoard-bolt  
依赖hightcharts组件jQuery.plugins.hightcharts-bolt
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_dashboardView.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.mode="view"
仪表板中的查看模式。

<video id="video1" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_dashboardEdit.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.mode="edit"
仪表板的编辑模式,面板内容可编辑，改变大小以及位置。

# 组件使用说明
## 使用环境
    <link rel="stylesheet" href="../css/common/awesome/css/font-awesome.min.css">(使用到加载图标)
    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/plugins/jQuery.plugins.dashBoard-bolt.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.dashBoard-bolt.js'></script>
    <!-- 使用gridstack.js的需要 -->
    <link rel="stylesheet" href="../css/common/gridstack/gridstack.css">
    <script type='text/javascript' src='../js/common/gridstack/jquery-ui.min.js'></script>
    <script type='text/javascript' src='../js/common/gridstack/lodash.min.js'></script>
    <script type='text/javascript' src='../js/common/gridstack/gridstack.all.js'></script>
    <script type='text/javascript' src='../js/common/gridstack/knockout-min.js'></script>
    <!-- 还需要引入hightcharts组件依赖的hightcharts库 -->

>[API](https://github.com/gridstack/gridstack.js)  
[API](https://github.com/gridstack/gridstack.js/tree/develop/doc)

## 方法

    <div class="dashBoard"></div>自定义class="dashBoard"用于方法调用

通过JavaScript调用菜单组件:

    $(".dashBoard").getDashboard([options,]dashboardData);

## 参数
### 1.dashboardData     
可以是制定格式的数据,亦可以是返回指定格式数据的Function,function中返回数据需要ajax请求结束后，可能需要使用同步请求方式(array/function).
#### 数据格式

    var dashboardData= [{
        "id":"panels1",//面板ID
        "title": "面积图-areachart-.highcharts(areaData,{export:true})",//面板标题
        "location": {//面板位置大小
            "dataGsX": 0,//X坐标
            "dataGsY": 0,//Y坐标
            "dataGsWidth":4,//宽度
            "dataGsHeight": 15//高度
        },
        "options":{export:true},//hightcharts组件options
        "widgets": [{//多组绘图数据
            "ajax":false,//flase:使用下面data数据;true:使用data值进行ajax请求数据
            "data":areaData[0]//object:数据格式同hightcharts组件的hightchartData中的对象数据;String:ajax请求路径
        },{
            "ajax":true,
            "data":"ajax请求路径"
        },
        ...
        ]
    },
        ...
        ]
    },
    ...
]

### 2.options  
options,非必传项(object)。

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| mode      | string        | false | "view"  |"view":查看模式;"edit":编辑模式|
| grid_options     | object       | false |     |gridstack.js基本信息配置|
| callback      | object        | false |   {}    |各种事件后的回调函数|

#### options.grid_options

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| verticalMargin      | number        | false | 15  |面板垂直间距|
| cellHeight     | number      | false |  2   |面板大小单位大小|
| handle     | string       | false |  ".drag-handle" |options.mode=="edit"时拖动元素|
| levelMargin     | number       | false |  15   |面板水平间距|

#### options.callback

| 名称          | 类型           | 参数  | 返回值 | 描述  |
| :-----------: |:-------------:| :-----  | :-----  |:-----|
| onDel        | function       | $this(本次删除的父级class=".grid-stack-item"元素),delArray(累计删除的面板id)    | 无 |options.mode=="edit"时删除面板的回调函数|

## 对象方法

| 方法名称          | 类型           | 返回值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| getAllWidgets      | function   | 返回现有的所有面板最新信息    |得到现有的所有面板最新信息|
| getAllHightchartId    | function   | 返回所有绘图面板id,除单值图    |得到所有绘图面板id,除单值图，如果页面大小发生改变，如菜单收缩，hightcharts就需要拿到这些id手动重绘更新图大小|

    var dashboardObj=$(".dashBoard").getDashboard([options,]dashboardData);
    var widgetsArray=dashboardObj.getAllWidgets();
    var hightchartIdArr=dashboardObj.getAllHightchartId();

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git
