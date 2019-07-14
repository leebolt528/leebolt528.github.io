---
title: input输入字段级联提示
tags:  ["promptExpre","plugin"]
comments: true
toc: true
---
# 前言
在外支援部门邻居项目组做搜索引擎那块时有一个这样的需求，一个input输入框，输入内容格式为 "字段 运算符 值 连接符 字段 ...".运算符的提示值由前面选择的字段决定，值的提示值由前面的字段+运算符决定，连接符后匹配规则重新开始,当然每个字段也可以手动输入，如果值需要手动输入日期格式时，时间应该使用双引号""包含。
<!-- more -->
# 组件
promptExpre组件jS.plugins.promptExpre-bolt.js
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_promptExpre.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

# 组件使用说明
## 使用环境

    <link rel="stylesheet" href="../css/common/commonBolt.css">(组件公共样式)
    <link rel="stylesheet" href="../css/plugins/jS.plugins.promptExpre-bolt.css">

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/plugins/jS.plugins.promptExpre-bolt.js'></scrip
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.relativeD3-bolt.js'></script>

## 方法

    <div class="autoInput"></div>自定义class="autoInput"用于方法调用

通过JavaScript调用菜单组件:

    $(".autoInput").promptExpre([options],promptExpreData);

## 参数
### 1.promptExpreData     
可以是制定格式的数据,亦可以是返回指定格式数据的Function,function中返回数据需要ajax请求结束后，可能需要使用同步请求方式(array/function).
#### 数据格式

    var promptExpreData = {
    "field": [  //字段值
        "fl_article_from",
        "fl_board_name",
        "fl_content",
        "fl_fetch_time"
    ],
    "fieldop": {//对应字段值后的运算符
        "fl_article_from": [
            "=",
            "!=",
            "is"
        ],
        "fl_content": [
            "=",
            "!=",
            ">",
            ">=",
            "<",
            "<=",
            "is"
        ],
        ...
    },
    "valuemap": {//字段+运算符后的值
        "fl_article_from#=": "contentop1",
        "fl_article_from#!=": "contentop2"，
        ...
    },
    "values": {
        "contentop1": {
            "type": "value",//使用下面的data值
            "data": [
                "新华网",
                ...
            ]
        },
        "contentop2": {
            "type": "http",//使用以下data请求ajax数据(请求后台路径为data+输入框中刚输入的运算符)
             "data":"ajax请求路径"
        },
        ...
    }
}

### 2.options
options,非必传项(object)。

| 名称          | 类型           | 必传 | 默认值  | 描述  |
| :-----------: |:-------------:| :----- |:-----  |:-----|
| callback      | object        | false |   {}    |各种事件后的回调函数|

#### options.callback

| 名称          | 类型           | 参数  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| onClickSearch      | function       | value(当前搜索框的值)  |点击搜索后回调函数|
| onClickClear    | function       |  无   |点击清空按钮后回调函数|

## 对象方法

| 方法名称          | 类型           | 返回值  | 描述  |
| :-----------: |:-------------:| :-----  |:-----|
| getInputValue      | function   | value     |获取当前搜索框的值|

    var promptExpreObj=$(".autoInput").promptExpre(options,promptExpreData);
    var value=promptExpreObj.getInputValue();

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git