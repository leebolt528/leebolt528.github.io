---
title: 左侧三级导航菜单组件（升级版本）
tags:  ["menu","plugin"]
comments: true
toc: true
---
# 前言
前段时间项目重构，于是我之前封装的左侧三级菜单派上了用场。由于前端页面有UI的设计，样式方面做了改动；在使用中功能上肯定也避免不了一定的升级优化。
<!-- more -->
# 组件
左侧三级菜单jQuery.plugins.menuLeft-boltNew
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_menuLeftShrink0.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.shrink=0
页面的独立框架使用的菜单模式。    
    
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_menuLeftShrink1.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.mode=1
页面的集成框架使用的菜单模式。

# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/plugins/jQuery.plugins.menuLeft-boltNew.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.menuLeft-boltNew.js'></script>

>去除font-awesome.min.css的引用，在数据项中使用class引入图片

## 方法

    <div class="menuLeft"></div>自定义class="menuLeft"用于方法调用

通过JavaScript调用菜单组件:

    $(".menuLeft").menuLeftBolt([options],menuLeftData);

## 参数
### 1.menuLeftData     
可以是制定格式的数据,亦可以是返回指定格式数据的Function,function中返回数据需要ajax请求结束后，可能需要使用同步请求方式(array/function).
#### 数据格式

    var menuLeftData=[
        {"id":"1","name":"时间选择","class":"menu-log-search","href":"selectTime.html","secUrl":"","param":{"aa":"11"},"children":[]},
        {"id":"2","name":"规则链库","class":"menu-log-perspect","href":"#","secUrl":"","param":{"aa":"11"},"children":[
            {"id":"2-1","name":"规则链库1","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[]},
            {"id":"2-2","name":"规则链库2","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[]},
            ...
        ]},
        {"id":"3","name":"设备管理","class":"menu-log-meter","href":"#","secUrl":"","param":{"aa":"11"},"children":[
            {"id":"3-1","name":"设备管理1","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[
                {"id":"3-1-1","name":"设备管理1-1","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[]},
                ...
            ]},
            {"id":"3-2","name":"设备管理2","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[]},
            {"id":"3-3","name":"设备管理3","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[]},
            {"id":"3-4","name":"设备管理4","class":"","href":"#","secUrl":"","param":{"aa":"11"},"children":[]},
            ...
        ]},
        ...
    ]


| 参数     | 类型       | 描述    |
| :------: |:---------:| :-----  |
| id       | string    | 每项菜单项的唯一标识  |
| name     | string    | 菜单项的名称   |
| fa       | string    | 菜单项名称前显示的awesome图标   |
| class       | string    | 菜单项名称前显示的图标,在css文件中定义图片引用   |
| secUrl     | string    | secUrl.length>0时，项目需要在可点击的菜单项外层包裹的sec标签控制权限，<sec:authorize  url=secUrl></sec:authorize>    |
| param     | string    | 绑定的对象参数，可以在回调函数的点击事件中获取使用    |
| children | array     | 该菜单下的子菜单    |

>去除参数"fa"  新增参数"class","secUrl","param"

### 2.options
options可不传将使用内置默认(object)。

| 名称          | 类型           | 默认值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| selected      | string        | null  |表示当前所在页,用于左侧菜单高亮,值为菜单项数据标识ID值|
| menuOpen      | boolean       |  true   |菜单初始化是否展开|
| hideFloat     | boolean       |  true   |点击向右浮出的菜单项,悬浮的菜单框是否消失|
| shrink      | number       |  0   |分别为三种模式：0-独立框架伸缩菜单 1-集成框架伸缩菜单 2-独立框架无伸缩菜单|
| title      | object       |  {}   |导航头部信息|
| callback      | object        |   {}    |各种事件后的回调函数|

>新增参数"shrink","title"

options.title。

| 名称          | 类型           | 默认值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| enabled      | boolean        | false  |是否显示头部信息|
| class      | string       |  ""   |头部图标|
| content      | string       |  ""   |头部标题|

#### options.callback

| 名称          | 类型           | 参数  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| onClick      | function       | $this,param     |点击选中菜单后的回调函数。$this:当前点击的元素;param:数据里传入的param对象,用于获取跳转页面需要的信息|
| onExpand      | function       | shrink     |点击展开菜单后的回调函数。shrink:options.shrink值,用于页面布局调整|
| onCollapse    | function       |  shrink    |点击收起菜单后的回调函数。shrink:options.shrink值,用于页面布局调整|

>增加onClick回调，onExpand和onCollapse添加返回参数。

## 对象方法

| 名称          | 参数           | 返回值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| updateTitle   | title(options.title)    | 无 | 用于修改头部标题|

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git
    





