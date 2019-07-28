---
title: 右侧滑出模态框组件
tags:  ["sideModal","plugin"]
comments: true
toc: true
---
# 前言
之前项目都是用的bootstrap弹出模态框，UI设计之后模态框都要从右侧滑出，所以这么频繁使用到的东西还时封装一下比较好,一劳永逸嘛，使用和维护都方便。
<!-- more -->
# 组件
右侧滑出模态框jQuery.plugins.sideModal-bolt
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_sideModal.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>
# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.sideModal-bolt.js'></script>

## 方法
>在页面加载开始执行$.sideModalFun(),否则页面首次弹出侧边栏无过渡效果

在点击事件中直接通过JavaScript调用组件:

    $.sideModalFun(options)

## 参数
### options
options可不传将使用内置默认(object为空)。

| 名称          | 类型           | 默认值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| headText      | string        | ""  |头部文本|
| btnSwitch      | boolean       |  true   |是否添加按钮|
| classList     | string       |  ""   |自定义的class,多个空格分开，默认designer_detail|
| imgPath      | string       |  ""   |关闭和加载图标的路径前缀|
| callback      | object        |   {}    |各种事件后的回调函数|

#### options.callback

| 名称          | 类型           | 参数  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| clickConfirm      | function       | $rightModel     |点击确认按钮后的回调函数|
| clickCancel      | function       | $rightModel     |点击取消，关闭按钮后的回调函数，默认消失|
| clickMask    | function       |  $rightModel    |点击阴影后的回调函数，默认消失|

>$rightModel是返回的右侧模态框。

## 对象方法

| 名称          | 参数           | 返回值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| showSideModal | 无            |    无   |右侧模态框和阴影出现|
| hideSideModal | 无            |    无   |右侧模态框和阴影消失|
| addHtml       | 需要添加的文本 |    无   |添加除头部和底部按钮的内容|
| getPaDom      | 无            |    无   |获取右侧模态框元素|

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git
    





