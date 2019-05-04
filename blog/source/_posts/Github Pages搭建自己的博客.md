---
title: 使用Hexo + Github Pages搭建个人独立博客
tags:  ["hexo","blog"]
comments: true
toc: true
---
# 1.前言
由于最近公司项目不是很紧张，想着梳理一下自己最近的收获和对技能方面有进一步系统的学习。突然发现了我确实有必要拥有一个自己的博客，于是最近一有空就会着手于这方面的研究。经过这么几天的纠结跳坑，通过阅读其他大神的分享我也终于搭建成功了自己的博客。
<!-- more -->
## 那么我为什么要建立自己的博客？
### 1.提高将事情讲清楚的能力
>将一件事情写下来，可以锻炼一个人的思维逻辑能力和提高表达分析能力，写会迫使你在你脑中搭建一个条理的框架。
>>如果一件事你没有讲清楚，十有八九是你还没有理解清楚。
### 2.培养持续做一件事的能力
>我大三曾经坚持健身一年，健身带来了我们所求所想的好；我想看书让自己的心静下来，可我怕买回来不看没勇气去买；但我从现在开始必须要坚持写博客，默默地持续做一件事是一种难得的能力，也是一种难得的品质,将会提供一股持续学习的动力。
>>开始是坚持，后来是习惯，接着是喜欢。
### 3.积累更多的知识
>之前总是断断续续地学习一些东西，等到真正使用时突然发现还得从头开始查阅学习，这样方式严重阻碍的个人的提升。因此我觉得我有必要记录自己曾经学习的知识，构建自己的学习体系。
>>写并不是单纯的写。
### 4.分享带来的连锁反应
>正如大家的学习主要依赖于网络其他朋友的分享，想我这次的搭建博客完全是依赖于他人的分享。
>>互联网给你的反馈就是让你承受更多，接受更多，成为一个更好的人。
### 5.记录成长
>回首自己写的博客，你将会发现自己正在通过这种方式不断的成长，这种成长在自己眼里是一笔财富，在别人眼里是一张地图，你得到的收获不断修正自己的错误，别人得到指引避免走弯路。
>>So what,that is what I am!
# 2.开始搭建Github Pages
## 1.使用前了解Github
>GitHub是一个共享虚拟主机服务，用于存放使用Git版本控制的软件代码和内容项目(引自维基百科）
## 2.为什么选择Github?
>github有一个很有爱的项目，叫做GitHub Pages,这个是给开发者建立的一个私人页面，上面用来分享新颖的想法和自己写的代码。而且最主要的是，这个是免费而且没有空间流量限制的。这也就是我为什么放弃了自由度很高的，却需要支付高昂的主机费的wordpress，而转投了github pages阵营。
## 3.注册github账号
[点击进行注册](https://github.com/)(此处不做详细说明可自行阅读[github教程：[1]注册github](http://jingyan.baidu.com/article/455a9950abe0ada167277864.html))

注册完毕后你就拥有了自己的代码仓库。
## 4.创建仓库
点击Github右上角加号选择New repositor(新存储库)或[点击这里](https://github.com/new)进行创建一个仓库。

![创建一个仓库](\img\blog\create1.png)
## 5.开启Github Pages
进入设置

![设置](/img/blog/create2.png)

找到这一块

![设置](/img/blog/create3.png) 

当你的仓库名为：用户名.github.io 之后默认开启Github Pages

现在随便选择一个主题,选择上图的 Choose a theme 之后会跳转到下面这个页面

![选择主题](/img/blog/create4.png) 

设置完毕后你就可以通过 username.github.io(username为你的用户名访问你的博客了)
# 3.hexo系统环境配置
要使用Hexo，需要在你的系统中支持Nodejs以及Git，如果还没有，那就开始安装吧！
## 安装Node.js
[下载Node.js](https://nodejs.org/en/download/)   
参考:[安装Node.js](http://www.runoob.com/nodejs/nodejs-install-setup.html)  
## 安装Git
[廖雪峰Git安装使用教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

[下载Git](https://git-scm.com/download/)  
一路点击Next就行了.

### 自报家门
    
    $ git config --global user.name "Your Name"
    $ git config --global user.email "email@example.com"

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。

注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
### 添加SSH Key到Github
第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

    $ ssh-keygen -t rsa -C "youremail@example.com"
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

第2步：登陆[GitHub](https://github.com/)，打开“settings”，“SSH and GPG keys”页面：

然后，点“New GPG key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

![添加公钥](/img/blog/key.png)

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

## 安装Hexo
在你需要安装Hexo的目录下(新建一个文件夹)右键选择 Git Bash 
    
    $ npm install hexo-cli -g   
    $ hexo init blog  #初始化网站
    $ cd blog   
	$ npm install   
	$ hexo g #生成静态文件，会在当前目录下生成一个新的叫做public的文件夹/ 或者 hexo generate
	$ hexo s #启动本地web服务，用于博客的预览 或者 hexo server,这一步之后就可以通过http://localhost:4000  查看了

*详细命令请参考[Hexo文档](https://hexo.io/docs/commands.html)* 

另外还有几个其它常用命令:
    
    $ hexo new "postName" #新建文章
    $ hexo new page "pageName" #新建页面

常用简写
    
    $ hexo n == hexo new #生成文章
    $ hexo c == hexo clean #清除缓存
    $ hexo g == hexo generate #保存修改，生成文件
    $ hexo s == hexo server #启动本地服务
    $ hexo d == hexo deploy #发布到远程
    $ hexo init #生成站点
    $ hexo new page "xxx" #生成页面
    $ npm install --save xxx  #安装插件
    $ npm unstall xxx #卸载插件

## 添加主题
### 安装主题（yilia）
    
    $ cd blog
    $ hexo clean
    $ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia

### 启用主题
找到目录下的_config.yml 文件,打开找到 theme：属性并设置为yilia
### 跟新主题

    $ cd themes/yilia
    $ git pull
    $ cd ../..
    $ hexo g
    $ hexo s

现在打开[http://localhost:4000](http://localhost:4000),会看到我们已经应用了一个新的主题。
# 4.使用Hexo deploy部署到github
这一步恐怕是最关键的一步了，让我们把在本地web环境下预览到的博客部署到github上，然后就可以直接通过[http://username.github.io](http://leebolt528.github.io)访问了。不过很多教程文章对这个步骤语焉不详，这里着重说下
### 首先需要明白所谓部署到github的原理
1. 之前步骤中在Github上创建的那个特别的repo(leebolt528.github.io)一个最大的特点就是其master中的html静态文件，可以通过链接 http://leebolt528.github.io 来直接访问。
2. hexo g 会生成一个静态网站(第一次会生成一个public目录),这个静态文件可以直接访问。
3. 需要将hexo生成的静态网站提交到github上.

### 使用hexo deploy部署
需要在blog的根目录下的配置文件_config.xml中作如下修改：
>deploy:    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type: git    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;repo: git@github.com:leebolt528/leebolt528.github.io.git  #这里的网址填你自己的    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branch: master

保存后运行一下命令即可完成部署：

    npm install hexo-deployer-git --save #必须在hexo d之前安装这个扩展
    hexo d
这时再刷新username.github.io就可以看到你的博客了。
# 5.关于hexo搭建博客后的一些基础配置
***一些配置需要在blog根目录和themes/yilia下的两个_config.yml文件中在修改。***
## 修改主题
1. 找到想要的主题后，下载到目录的themes下 
```
    git clone https://github.com/wuchong/jacman.git themes/jacman
```
2. 修改全局config.yml中的theme,theme:yilia 把yilia改为pacman.
3. 然后进行主题更新以及部署(最后上传到github).
```
    cd themes/jacman
    git pull
    hexo clean
    hexo d -g
```
## 使用畅言评论
### 方式一
注册[畅言](http://changyan.kuaizhan.com/)后，在themes/主题下的.config.yml中修改一下字段:
>#畅言    
changyan_appid: cysWBK2R1  #你在注册畅言中得到的APP ID  
changyan_conf: c0d676145cb5b4242cedcdef8d2e97d6 #你在注册畅言中得到的APP KEY 

在每篇文章开头的 front-matter 中添加一句comments: true，然后回到博客根目录执行命令 hexo d -g ，重新生成博客并部署博客，然后刷新，任选一篇文章进入下拉，会发现评论功能可以使用了。

![comments: true](/img/blog/changyan.png)
### 方式二
[Hexo博客yilia主题更换畅言评论系统](http://www.luck666.cn/2017/03/22/hexo-yilia-changyan/)

[在Hexo中使用畅言评论系统](https://www.lichanglin.cn/%E5%9C%A8Hexo%E4%B8%AD%E4%BD%BF%E7%94%A8%E7%95%85%E8%A8%80%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/)
## hexo yilia 文章目录
[Hexo + yilia 主题实现文章目录](http://www.54tianzhisheng.cn/2017/06/13/Hexo-yilia-toc/)
## yilia标签分类
如果要有多个标签，可以如下图所示：

![tags](/img/blog/tags.png)
## hexo yilia 设置文章显示长度，不展开全文
![截取文章长度](/img/blog/more.png)
## hexo yilia 怎么写文章
我一般写文章就是先用本地 markdown 编辑器写好后，然后放在 hexo 的 source/_posts 目录下。
## 不知道如何编写Markdown语法
[Markdown——入门指南](https://www.jianshu.com/p/1e402922ee32/)

[Markdown 中文版语法说明](http://wowubuntu.com/markdown/#list)
## 草稿（私密文章）
我们可以在blog的source下创建一个_drafts文件夹，用于保存不舍得删除的。但也不想在页面上显示的文章，或者比较私人的不想让其他人看到的文章。如果要强制预览，可以在blog目录下的.config.yml中强制开启。
>render_drafts: false #强制预览修改为true
## 添加站长统计
进入[cnzz](http://www.umeng.com/)进行注册和相应的设置

![cnzz账号注册](/img/blog/cnzz1.png)
#### 方式一：（亲测无效）
在给出的代码中复制出id，把id填入到主题里的config.yml中对应的cnzz位置，如下
>cnzz_tongji:    
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enable: true    
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;siteid: 12733***** 
#### 方式二
![cnzz代码获取](/img/blog/cnzz2.png)

获取自己喜欢的代码填入/blog/themes/yilia/layout/_partial/footer.ejs中的`</footer>`标签前。接着访问username.github.io就可以看到页面底部为下图所示：

![cnzz查看分析](/img/blog/cnzz3.png)

点击新出现的图标即可查看分析，可以如下图所示按需设置查看密码。

![cnzz查看密码](/img/blog/cnzz4.png)
## 添加百度统计分析
进入[百度分析](https://tongji.baidu.com/web/25415468/welcome/login)进行注册和相应的设置

![百度分析注册](/img/blog/baidu1.png)

![百度分析注册](/img/blog/baidu2.png)

![百度分析注册](/img/blog/baidu3.png)
#### 方式一
在给出的代码中复制出id，把id填入到主题里的config.yml中对应的cnzz位置，如下
````
# Miscellaneous
baidu_analytics: '8678388163569xxxxxxxx'
google_analytics: 'UA-9700xxxxxxxx'
````
#### 方式二
直接把上述代码粘贴到/blog/themes/yilia/layout/_partial/head.ejs中的`</head>`标签前。接着就可以去该网站登陆自己的账号查看分析了。

## RSS订阅
添加rss订阅，需要安装插件

    npm install hexo-generator-feed --save
接着在blog目录下的config.yml中添加`rss: /atom.xml #rss地址  默认即可`。这样，rss订阅功能就开启了。
## 电脑重装了系统/多台电脑写博客？
完成Hexo本地运行后，会在本地文件里生成一个public文件夹。public文件夹内是根据.md生成的html文件，也就博客的静态文件。

通常情况下，我们执行：`$ hexo d`,就是把public文件夹下的文件同步到github，然后就能通过https://username.github.io/访问博客了。所以，我们的思路其实就是把静态文件和Hexo环境，分别存在username.github.io的master和hexo分支上。

![博客分支存储](/img/blog/branch.png)

>1.创建仓库--username.github.io;    
2.创建两个分支：master 与 hexo;(git branch hexo创建,git checkout hexo切换)    
3.设置hexo为默认分支(因为我们只需要手动管理这个分支上的Hexo网站文件);    
4.使用git clone git@github.com:username.github.io.git拷贝仓库;    
5.在本地http://username.github.io文件夹下通过Git bash依次执行安装Hexo和添加主题命令(此时当前分支应显示为hexo);    
6.修改根目录下的_config.yml中的deploy参数，分支应为master;    
7.依次执行git add .、git commit -m "..."、git fetch&&git rebase、git push origin hexo提交网站相关的文件;    
8.执行hexo g -d生成网站并部署到GitHub上。

*blog中的子文件夹中.git需要删除，否则导致提交部署不成功*
之后只需要每次在本地的blog文件下进行文章的增删改操作,完了提交到hexo分支上，再部署到远程master分支上即可。
## hexo yilia 引入音乐
```
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="填写音乐链接地址"></iframe>
```
如下图，可以在网易云音乐里搜到你想要引入的音乐，然后点击如下的 “生成外链播放器” 即可：

![网易云](/img/blog/music1.png)

![网易云](/img/blog/music2.png)
## hexo引入视频
```
<iframe height="80%" width="80%" src="http://player.youku.com/embed/XMjUzMzY4OTM3Ng==" 
	frameborder=0 allowfullscreen>
</iframe>
```
