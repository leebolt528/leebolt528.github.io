---
title: highcharts组件
tags:  ["highcharts","plugin"]
comments: true
toc: true
---
# 前言
去年的一个里程碑中，项目中有大量使用到图表。为了提高在后续开发过程中的一致性，高效性和维护性，于是把highcharts库中常用的一些图表进行了封装，确实对后来的开发提供了的极大的便利性。然而由于兼容了许多类型的图表，虽然在开发过程中想了很多，在后续实际生产环境中仍然接连暴露出很多意想不到的BUG，正因为如此之后的维护也花费了一些时间，最终也算比较稳定和成熟了。<span style="color:red">该组件某些图表类型数据格式还不是很一致，文档不够详细，接下来会尽快调整完善！！！</span>
<!-- more -->
# 组件
hightcharts组件jQuery.plugins.hightcharts-bolt
# 组件效果展示
<video id="video" controls="controls"   preload="preload" poster="\img\public\head.jpg">
    <source id="mp4" src="\video\plugin\Video_highcharts.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/ 05/sintel/trailer.ogv" type="video/ogg">
</video>

# 组件使用说明
## 使用环境

    <script type='text/javascript' src='../js/common/jquery/jquery.min.js'></script>
    <script type='text/javascript' src='../js/common/highcharts/highcharts.js'></script>
    <script type='text/javascript' src='../js/plugins/jQuery.plugins.highcharts-bolt.js'></script>
    /*以下文件可以按需加载*/
    <script type='text/javascript' src='../js/common/highcharts/drilldown.js'></script>//下钻图表
    <script type='text/javascript' src='../js/common/highcharts/highcharts-more.js'></script>//气泡图
    <script type='text/javascript' src='../js/common/highcharts/no-data-to-display.js'></script>//无数据时显示提示
    <script type='text/javascript' src='../js/common/highcharts/solid-gauge.js'></script>//仪表图
    <script type='text/javascript' src='../js/common/highcharts/oldie.js'></script>//词云图
    <script type='text/javascript' src='../js/common/highcharts/wordcloud.js'></script>//词云图
    /*以下三个文件在开启图表导出功能时使用(options.export=true时)*/
    <script type='text/javascript' src='../js/common/highcharts/exporting.js'></script>//导出图表
    <script type='text/javascript' src='../js/common/highcharts/offline-exporting.js'></script>//导出图表
    <script type='text/javascript' src='../js/common/highcharts/highcharts-zh_CN.js'></script>//导出图表汉化

>[Hightcharts](https://www.highcharts.com.cn/)  
如果项目中有使用bootstrap时，加入以下样式解决bootstrapy对导出列表样式的冲突
 ```
    //在开启图表导出功能时使用(options.export=true时)
    <style type="text/css">
    .highcharts-contextmenu hr{
        margin:0px!important;
    }
    </style>
```

## 规范说明
>1. Y轴支持数值类型数据,后台可以返回number和string随意类型,无值时返回null或"null";
2. X轴支持时间戳,字符串和数值类型,时间戳(秒级)和数字类型可以返回number和string随意类型;
3. 所有的百分比堆叠图,饼图和双环扇形图返回的Y值需是实际值,单位是实际单位;
4. 组件会对数值类型进行小数点保留处理;
5. 无数据时data,result和values都可以任意为null||"null"||[],values的y值无值时为null||"null";
6. 词云图字段分割通过"," "."或" "分割;
7. 特殊单位标准：内存大小单位-KiB,KiB/s,s;(比如只要是时间类型的数值都传入以秒为单位的数值，然后交由组件内部处理自适应转换单位)
8. 建议直接查看实例数据使用会更加准确快捷;
9. 通过配置options参数，几乎可以改变任何样式，得到符合自己需求和审美的图。

## 方法

    $("#ID/.class").highcharts([options,]hightchartData);

## 参数
### 1.hightchartData
可以是制定格式的数据,亦可以是返回指定格式数据的Function,function中返回数据需要ajax请求结束后，可能需要使用同步请求方式(array/function).
#### 数据格式

    var hightchartData=[
        {
            "label":{//非第一组数据label下只需要设置seriesReg字段，其余共用第一组数据的label设置。
                "seriesReg":"{{monitor_host}}:{{job}}",//数据项名称规则，使用{{}}包含result里的seriesAttr的属性名称以获取值。因为数据项名称有时后台不可以直接返回，需要拼接
                "yAxisUnit":"容量-s",//y轴名称和单位，名称和单位为空时，值为"-".
                "xAxisUnit":"-",//X轴名称和单位(单位如KiB,KiB/s/s)
                "zAxisUnit":"-",//X轴名称和单位,散点图和气泡图会用到.
                "xAxisType":"dataTime",//X轴数据类型(时间类型为“dataTime”,数值类型为“number”(数值可以加引号但属于number类型)),字符串类型为“string”;饼图和双环图值不使用字段，值随意)
                "type":"areachart",//图表类型
                "title":"内存大小",//图标题名称
                "outerData":[['健康','20'],['良好',50],['一般',30]],//外环数据(只双环图需要，数组长度为三,值只需成比例即可).
                "drillData": [{ //只下钻饼图所需要的二级，三级..数据
                    id: 'dazhong',
                    data: [
                        {
                            name: '一汽',
                            y: 100
                        },{
                            name: '上汽', 
                            y:100,
                            drilldown: 'shangqi'
                        }
                    ]
                }, {
                    id: 'bentian',
                    data: [{
                        name: '雅阁',
                        y: 120
                    },{
                        name: 'CR-V', 
                        y:30
                    }]
                }, {
                    id: 'xuefulan',
                    data: [
                        ['科鲁兹', 50],
                        ['迈锐宝XL', 40],
                        ['探界者', 10]
                    ]
                },{
                    id: 'shangqi',
                    data: [
                        ['帕萨特', 70],
                        ['辉昂', 20],
                        ['途观', 10]
                    ]
                }]
            },
            "result":[//当为双环扇形图时多组数据result下的values总个数为2
                {
                    "seriesAttr":{     //数据项名称字段
                        "monitor_host":"172.16.26.41",
                        "instance":"172.16.26.41:9990",
                        "monitor_env":"kafka41",
                        "monitor_port":"9092",
                        "monitor_cluster":"blogic-kafka-cluster",
                        "job":"kafka_jmx",
                        "monitor_type":"MQ"
                    },
                    "values":[    //数据值(当为饼图或环状图时values长度为1且数组第一个为空字符串"",当饼图和柱形图下钻时增加第三个为id或空字符串"".无数据时为null或[])
                        ["1536029467","486132.72"],["1536029468.5","486132.72"],["1536029470","486132.72"],["1536029471.5","625963.9"],["1536029473","625963.9"],["1536029474.5","625963.9"]
                },
                {
                    "seriesAttr":{                 
                        "monitor_host":"172.16.3.117",
                        "instance":"172.16.3.117:9990",
                        "monitor_env":"kafka117",
                        "monitor_port":"9092",
                        "monitor_cluster":"blogic-kafka-cluster",
                        "job":"kafka_jmx",
                        "monitor_type":"MQ"
                    },
                    "values":[
                        ["1536029467","685986.69"],["1536029468.5","685986.69"],["1536029470","685986.69"],["1536029471.5","685986.69"],["1536029473","685986.69"],["1536029474.5","685986.69"]
                    ]
                }
            ]

        },//第一组数据
        ...
    ]

>**label.type说明：**
面积图-"areachart";曲线面积图-"areasplinechart";百分比面积图-"areachartpercent";堆叠面积图-"areachartnormal";
折线图-"linechart";曲线图-"splinechart";柱状图-"columnchart";百分比柱状图-"columnchartpercent";堆叠柱状图-"columnchartnormal";可下钻柱状图-"columnchartdrill";
条形图-"barchart";百分比条形图-"barchartpercent";堆叠条形图-"barchartnormal";
散点图-"scatterchart";气泡图-"bubblechart";饼图-"piechart";可下钻饼图-"piechart"(与饼图相同，只是属性多一个数据项drillData和values元素多一个参数);环形图-"piechartring";双环图-"piechartringrule";)
百分比活动图-"solidgaugechartpre";百分比活动图in-"solidgaugechartpreIn";百分比活动图out-"solidgaugechartpreOut";数值活动图-"solidgaugechartnum";数值活动图in-"solidgaugechartnumIn";数值活动图out-"solidgaugechartnumOut";
"百分比仪表图"-"gaugechartpre";"百分比仪表图out"-"gaugechartpreOut";"数值仪表图"-"gaugechartnum";"数值仪表图out"-"gaugechartnumOut";
词云图-"wordcloudchart";单值图-"singleValuechart"
**定义如此多的类型就是为了减少option参数的配置，降低使用难度**
### 2.options
options,非必传项(object)。
    
    var options={
            zoomType:"xy",//图表缩放类型（沿X轴-"x";沿Y轴-"y";沿XY-"xy";关闭-null）
            export:false,//是否开启导出图表功能
            lineWidth:1.7,//直线图和曲线图线的粗细
            cursor:'pointer',//光标形状(可点击-"pointer";无绑定事件-null)
            gaugeLevel:[50,30,20],//仪表盘颜色变化标准,数值大小成比例即可
            title: {//图表名称样式
                enabled:false,
                align: 'left',
                color: '#55B951',
                fontSize:'14px'
            },
            legend:{//图例说明样式
                enabled:true,
                fontWeight:"normal",
                fontSize:"12px",
                color:'#000',
                navEnabled:true,
                navHeight:40,
                y:0
            },
            labels: {//刻度名称样式
                color: "#666666", 
                fontSize: "12px" ,
                fontWeight:"normal"
            },
            stackLabels: {//堆叠数据标签(未优化)
                enabled: false,
                color: "contrast",
                fontSize: "11px",
                fontWeight: "bold"
            },
            dataLabels: {//数据标签样式
                enabled: false,//(双环图内部默认false不可配置)
                color: "contrast",
                fontSize: "11px",
                fontWeight: "bold",
                distance:30
            },
            marker:{
                enabled:false,//点标记是否开始
                radius:5//点的大小
            },
            tooltip: {//提示框样式
                enabled:true,
                shared: true,//false显示仪表盘中心文字附加行
                color: "#333333", 
                fontSize: "12px",
                whiteSpace: "nowrap",
                fontWeight:"normal"
            },
            xAxis:{
                enabledTitle:true,//X轴名称是否显示
                xTitleUnit:true//X轴单位显示位置(X轴名称后面-true,X轴刻度后面-false;)
            },
            yAxis:{
                enabledTitle:true,//Y轴名称是否显示
                yTitleUnit:false//Y轴单位显示位置(Y轴名称后面-true,Y轴刻度后面-false;)
            },
            color:["#64bcff","#0dd8d1","#ff7f31", "#d84d4d", "#8085e9",
            "#90ed7d", "#f15c80", "#e4d354","#91e8e1",
            '#4572A7', '#AA4643', '#89A54E', '#80699B', '#3D96AE',
            '#DB843D', '#92A8CD', '#A47D7C', '#B5CA92'],
            colorRule:['#38ae33','#ef8f40','#f64a4a',"#e6e6e6","#f4a6c4"],//双环图和仪表盘图颜色(前三个刻度等级颜色，第四个面板背景色，第五个刻度背景色)
            size:'100%',//扇形图，环图，仪表盘图大小
            ring:{//环形图特殊样式(饼图和仪表盘)
                startAngle:0,//-135起始角度
                endAngle:360,//135终止角度
                center:['50%', '50%']//图中心位置
            },
            pieRing:{//环形饼图特殊样式
                subEnabled:true,//中心文字是否显示
                subY:-10,//中心文字Y坐标
                subfontSize:'15px',//中心文字大小
                subunitSize:'20px',//中心单位字体大小
                subfontWeight:700,//中心文字粗细
                subColor:"#333333",//中心文字颜色
                innerSize:'65%',//内环粗细
                outerSize:'90%',//外环粗细
            },
            solidgauge:{//仪表盘特殊样式
                labelY:-22,//中心文字Y坐标
                dlfontSize:'30px',//中心文字大小
                dlunitSize:'20px',//中心单位字体大小
                dlfontWeight:700,//中心文字粗细
                dlBottomfontSize:'20px',//中心文字附加行字体大小
                panelOuterRadius:'100%',//面板宽度外界
                dataOuterRadius:'100%',//数值宽度外界
                plotOuterRadius:'100%',//刻度宽度外界

                panelInnerRadius:'75%',//面板宽度内界
                dataInnerRadius:'75%',//数值宽度内界
                plotInnerRadius:'75%',//刻度宽度内界
                ylabelsEnabled:true,//刻度数值是否显示
                ylabelsY:15,//刻度数值Y坐标
                ylabelsColor:"#666666",//刻度数值颜色
                ylabelsFontSize:"11px",//刻度数值字体大小
                tickAmount:0,//刻度总数
                minorTickWidth: 1,//次刻度线宽度
                minorTickLength: 10,//次刻度线长度
                minorTickColor: '#999999',//次刻度线颜色
                tickWidth: 2,//刻度线宽度
                tickLength: 15,//刻度线长度
                tickColor: '#ffffff',//刻度线颜色
                titleY:10,//单位Y坐标
                titleSize:"14px",//单位字体大小
                dialBaseLength:"60%",//指针长度
                dialRearLength:"15%"//指针长度
            },
            gauge:{//带指针仪表盘特殊样式
                labelY:-10,//中心文字Y坐标
                dialColor:"#0f0f0f",//指针颜色
                dialSize:4//指针粗细
            },
            singleValue:{//单值图特殊样式
                fontSize:'30px',//中心数值字体大小
                unitFontSize:'20px',//后缀字体大小
                fontWeight:700,//字体粗细
                color:"#333"//字体颜色
            }
       };

## 代码地址
>https://github.com/leebolt528/blogic-plugins.git