---
title: raphael编排+活动图组件
tags:  ["raphael","plugin"]
comments: true
toc: true
---
# 前言
raphael.js同D3.js一样都是基于SVG画布的。主要使用raphael实现了组件的编排(左侧拖取组件元素使用jquery-ui.min.js中的draggable和droppable)和编排运行后的活动图状态展示(需要编排过成生成的节点位置等信息)。
<!-- more -->
# 组件
raphael编排+活动图组件jQuery.plugins.rephael-bolt
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_raphaelMapping.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.model=null
编排生成关系图,包括映射等信息。    
    
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_raphaelState.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

>option.model="state"
加入状态事件等信息后的回显活动图。

><span style="color:red">因为业务性较强,所以是在项目中直接开发的，尽快整理出来一份，不过此文档主要针对option.model="state"的说明！！！</span>

# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/plugins/jQuery.plugins.raphael-bolt.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.raphael-bolt.js'></script>

>[raphael官网](http://dmitrybaranovskiy.github.io/raphael/)  
[raphael基础1](https://www.jianshu.com/p/1acf11dea10e)
[raphael基础2](https://www.jianshu.com/p/1acf11dea10e)
[raphael文档2](https://www.jianshu.com/p/ad139e13bbd0)    
[raphael避免入坑点](http://blog.sina.com.cn/s/blog_6f0e8cc10101k1wx.html)