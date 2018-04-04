---
title: gulp项目使用讲解
tags: ["tools","gulp"]
toc: true
---
# 引言
在工作中经常会有对静态资源合并和压缩的操作。[gulp](https://www.gulpjs.com.cn/)是基于Nodejs在前端开发过程中对代码进行构建的工具，是自动化项目的构建利器，她能自动化地完成 javascript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。gulp 和 grunt 非常类似，但相比于 grunt 的频繁 IO 操作，gulp 的流操作，能更快地更便捷地完成构建工作。
<!--more-->
# 正文
## 安装node.js
由于gulp使用基于node，所以首先要安装[node环境](https://nodejs.org/en/)。
## 安装Gulp环境
    $ npm install gulp -g
## 项目中使用Glup
1. 在项目根目录下写命令行 初始化：`npm init` , 此时根目录会出现package.json.
2. 进入项目的适当位置（一般为根本目录或前端代码的最上层），运行安装本地Gulp环境，运行命令：
```
$ npm install gulp --save-dev
```
3. 安装css,js压缩的环境，运行命令：
```
$ npm install gulp-uglify --save-dev #局部安装gulp-uglify(压缩JavaScript)
$ npm install gulp-clean-css --save-dev #局部安装gulp-clean-css(压缩css,或使用gulp-minify-css)
$ npm install gulp-concat --save-dev #局部安装gulp-concat(合并文件)
$ npm install gulp-rename --save-dev #局部安装gulp-rename(重命名)
$ npm install del --save-del #局部安装del(文件删除)
$ npm install gulp-uncss --save-dev #局部安装gulp-uncs(删除css冗余代码)
```
4. package.json 同级目录创建gulpfile.js,配置信息如下：
```
var gulp = require('gulp'),
    uglify = require('gulp-uglify'),
    cleancss = require('gulp-clean-css'),
    rename = require('gulp-rename'),
    del = require('del'),
    concat = require('gulp-concat'),
    uncss = require('gulp-uncss');
#合并压缩js
gulp.task('jsmin', ["clean"],function () {
    gulp.src(['WebContent/js/search/*.js']) #多个文件以数组形式传入
    .pipe(concat('search.js')) #把search下的js合并为search.js
    .pipe(gulp.dest('WebContentSrc/js')) #把合并后的search.js输出到WebContentSrc下
    .pipe(uglify()) #压缩search.js
    .pipe(rename({suffix: '.min'})) #压缩文件命名search.min.js
    .pipe(gulp.dest('WebContentSrc/js')); #把压缩文件search.min.js输出到WebContentSrc下
});
#单个压缩css
gulp.task('cssmin',["clean"], function () {
      gulp.src(['WebContent/css/**/*.css'])
     .pipe(gulp.dest('WebContentSrc/css')) 
     .pipe(rename({suffix: '.min'}))   
     .pipe(cleancss())
     .pipe(gulp.dest('WebContentSrc/css'));
});
#删除冗余css代码
gulp.task('uncssout', function() {
    gulp.src(['WebContent/css/**/*.css']) 
    .pipe(uncss({
        #使用css的html页面，可多个
        html: ['WebContent/views/*.html','WebContent/views/**/*.html','WebContent/views/**/**/*.html']
    }))
   #输出目录
   .pipe(gulp.dest('WebContent/css'));
});
#执行压缩前，先删除以前压缩的文件
gulp.task('clean', function() {
      return del(['WebContentSrc/css', 'WebContentSrc/js'])
});
#默认任务
gulp.task('default', function(){
      gulp.run('uncssout','jsmin', 'cssmin');
});
```
5. 直接运行gulp命令。

![gulp命令项目目录](/img/gulp/gulp.png)
