---
title: 左侧三级导航菜单组件
tags:  ["menu","plugin"]
comments: true
toc: true
---
# 前言
之前的项目中自己也封装了一些比较实用的小组件,一直想整理来着就这样拖到了来年。我终于不能忍自己啦，虽然最近项目上不算轻松，但我还是毅然决然地开始了“蓄谋已久”的事情来告别拖延。然而却发现之前的代码写的是多么潦草和随意，简直不忍直视，就这样接下来也花费了远比我预估多多的时间。
<!-- more -->
# 组件
左侧三级菜单jQuery.plugins.menuLeft-bolt
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_menuLeft.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/awesome/css/font-awesome.min.css">(组件中有使用此图标)
    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/plugins/jQuery.plugins.menuLeft-bolt.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.menuLeft-bolt.js'></script>

## 方法

    <div class="menuLeft"></div>自定义class="menuLeft"用于方法调用

通过JavaScript调用菜单组件:

    $(".menuLeft").menuLeftBolt([options],menuLeftData);

## 参数
* menuLeftData     
可以是制定格式的数据,亦可以是返回指定格式数据的Function(array/function).
* options
options可不传将使用内置默认(object)。

| 名称          | 类型           | 默认值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| selected      | string        | "null"  |表示当前所在页,用于左侧菜单高亮,值为菜单项数据标识ID值|
| menuOpen      | boolean       |  true   |菜单初始化是否展开|
| hideFloat     | boolean       |  true   |点击向右浮出的菜单项,悬浮的菜单框是否消失|
| callback      | object        |   {}    |各种事件后的回调函数|

* 2. options.callback

| 名称          | 类型           | 返回值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| onExpand      | function       | 无     |点击菜单向右展开后的回调函数|
| onCollapse    | function       |  无    |点击菜单向左收缩后的回调函数|
## 数据格式

    var menuLeftData=[
        {"id":"1","name":"时间选择","fa":"fa-home","href":"selectTime.html","children":[]},
        {"id":"2","name":"规则链库","fa":"fa-link","href":"#","children":[
            {"id":"2-1","name":"规则链库1","fa":"fa-home","href":"#","children":[]},
            {"id":"2-2","name":"规则链库2","fa":"fa-home","href":"#","children":[]},
            ...
        ]},
        {"id":"3","name":"设备管理","fa":"fa-link","href":"#","children":[
            {"id":"3-1","name":"设备管理1","fa":"fa-home","href":"#","children":[
                {"id":"3-1-1","name":"设备管理1-1","fa":"fa-home","href":"#","children":[]},
                ...
            ]},
            {"id":"3-2","name":"设备管理2","fa":"fa-home","href":"#","children":[]},
            {"id":"3-3","name":"设备管理3","fa":"fa-home","href":"#","children":[]},
            {"id":"3-4","name":"设备管理4","fa":"fa-home","href":"#","children":[]},
            ...
        ]},
        ...
    ]


| 参数     | 类型       | 描述    |
| :------: |:---------:| :-----  |
| id       | string    | 每项菜单项的唯一标识  |
| name     | string    | 菜单项的名称   |
| fa       | string    | 菜单项名称前显示的awesome图标   |
| href     | string    | 点击后需要跳转的对应页面    |
| children | array     | 该菜单下的子菜单    |

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git
    





