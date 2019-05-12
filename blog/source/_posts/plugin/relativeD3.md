---
title: D3关系图组件
tags:  ["menu","plugin"]
comments: true
toc: true
---
# 前言
由于关系图的灵活度较高，具体规则需求不一致，一般而言任何库估计也没有封装好的成品。于是我使用了免费并且灵活度很高的D3.js绘制关系图，期间需求一直该改改，但最终确实也没运用到生产环境中去，不过我还是将自己写的这部分总结了一下。
<!-- more -->
# 组件
relativeD3组件jQuery.plugins.relativeD3-bolt
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_relativeD3Line.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.mode="line"
重点展示数据中edges中的status,关系线根据status值不同呈现不同的颜色。

<video id="video1" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_relativeD3Node.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.mode="node"
重点展示数据中nodes中的status,节点边框根据status值不同用faultColor值颜色高亮，并且显示直线此节点的关系线同样显示不可使用。

# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type="text/javascript" src="../js/common/D3/d3.min.js"></script>(d3库)
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.relativeD3-bolt.js'></script>

## 方法

    <div id="canvas"></div>自定义id="canvas"用于方法调用

通过JavaScript调用菜单组件:

    $.relativeD3(id,d3Data,[options]);

## 参数
### 1.id  
容器id值
### 2.d3Data     
可以是制定格式的数据(object).
#### 数据格式

    var d3Data={
        "nodes": [{
                "name": "存量营销(同网)",//节点名称
                "image": "../img/plugins/relativeD3/user.png",//节点图片
                "key": "11",//节点唯一标识id
                "status": "1"//节点状态 0:正常;1:不正常，此属性仅在options.mode=="node"下使用
            }, {
                "name": "营销活动接口服务",
                "image": "../img/plugins/relativeD3/tomcat.png",
                "key": "22",
                "status": "1"
            },
            ...
        ],
        "edges": [{
                "source": "00",//关系线的入口节点,值为节点的key值
                "target": "11",//关系线的出口节点
                "relation": "17",//关系线上展示的信息
                "status": "fast"//关系线的状态"fast","slow","normal",此属性仅在options.mode=="line"下使用
            },
            ...
        ]
    }

### 3.options
options,非必传项(object)。

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| style      | object        | false |   |交互过程中的样式颜色|
| blankClear     | boolean       | false |  true   |点击画布空白处,是否清除选中的节点和关系线效果|
| modalSwitch     | boolean       | false |  false   |点击节点和线是否出现模态框|
| mode     | string       | false |  "node"   |共有"line"和"node"两个值,这两种模式下图的展示侧重点不同|
| freedom     | boolean       | false |  false   |是否允许元素可以出现在可是范围以外|
| callback      | object        | false |   {}    |各种事件后的回调函数|

#### options.style

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| lineColorNor      | string        | false | "#A9A9A9"  |edges.status=="normal"的线颜色(options.mode=="line");关系线颜色(options.mode=="node")|
| lineColorSlow     | string      | false |  "#CC0000"   |edges.status=="slow"的线颜色(options.mode=="line")|
| lineColorFast     | string       | false |  "#228B22"   |edges.status=="fast"的线颜色(options.mode=="line")|
| highLColor     | string       | false |  "#0099CC"   |点击悬浮高亮颜色|
| textColor     | string       | false |  "#696969"   |文本颜色|
| fillColor     | string       | false |  "#ccc"   |节点背景色|
| faultColor      | string        | false | "#CC0000"  |问题节点node.status=1标识颜色(options.mode=="node")|
| strokeW      | number        | false |   0   |节点边框宽度|

#### options.callback

| 名称          | 类型           | 参数  | 返回值 | 描述  |
| :-----------: |:-------------:| :-----  | :-----  |:-----|
| onClickNode      | function       | node(当前点击的节点对象)    | 需要在弹出模态框中添加的html |点击节点后的回调函数|
| onClickEdge    | function       |  edge   | 需要在弹出模态框中添加的html |点击关系线后的回调函数|
| onClickCanvas    | function       |  无   | 无 |点击空白画布后的回调函数|

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git