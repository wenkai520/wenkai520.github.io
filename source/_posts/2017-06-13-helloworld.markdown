---
layout: post
title: "使用github和OctoPress搭建个人博客"
date: 2017-06-14 20:43:00 +0800
comments: true
categories: 
---

以前在CSDN上有过个人blog，偶尔写写一些东西，但无奈动力不足。最近看到stormzhang开发者的一个公众号的内容，给人眼前一亮，上面有提到用OctoPress来搭建自己的blog。很是兴奋，也琢磨着自己也弄一个blog玩玩，刚好利用闲暇时间做一些思考，多做一些整理知识的时间，好处多多。说做就做，一开始想着这玩意估计没那么麻烦，怎奈花费了将近陆陆续续7-8个晚上的时间才搞的差不多。

在网上找了一些教程，可是写的说实话，我这新手看的不太懂，只能好几篇教程对比着看，一边Google，一边实践，才大概明白原理。

我到现在也是理解个皮毛，如果后面用熟悉了才会好点吧。
github上我们会建一个repo 仓库，相当于一个管理我们blog的仓库；
我们通过用cmd Markdown编辑阅读器把我们要写的博客内容编辑好之后，提交到github上的repo仓库里面就可以了。

主要参考了以下教程：
1.[Windows下OctoPress环境搭建][1]
2.[使用github + Octopress 搭建免费博客 + 碰到问题的解决方法][2]
3.[Running Jekyll with GitHub Pages using Windows 8.1 x64 and Ruby 2.0 x64][3]
4.[搭建OCTOPRESS][4]

具体安装步骤如下：
 ****1. 下载安装Git客户端** 
    https://git-for-windows.github.io/
    安装好之后鼠标右击会有GitBash Here的快捷方式，刚开始我的电脑有问题装完软件后什么软件都找不到，以前win10升级给升坏了，无奈重新装了一遍系统才正常。
 ****2.安装git后需要配置ssh**
打开GitBash,启动shell命令行后，输入命令：
    `ssh-keygen -C github-account-email -t rsa`
Note: username@email.com需要更换成你自己的在Github上注册的Email地址。 这样会在用户目录(C:\Documents and Settings\UserName)下产生一个.ssh文件夹，里面为对应的SSH Keys，其中id_rsa.pub是Github需要的SSH公钥文件。

在Github的Account Settings里选择SSH Keys，在其中将id_rsa.pub文件里内容拷贝至 其中的Key里。

这样以后就可以直接使用Git和GitHub了。

测试一下
`ssh -T git@github.com`

如果出现 hi xxx! You’ve successfully authenticated, bug GitHub does not povide shell access。说明SSH链接成功。

**3.克隆Repo到本地**

在D盘新建一个文件夹，例如GitHub。
`cd d:\GitHub
git clone git@github.com:username/username.github.com.git`

****4.安装ruby x64和DevKit x64 ****
使用RubyInstallers来安装ruby，可以在
https://rubyinstaller.org/downloads/archives/
中选择你所需要的ruby版本和DevKet版本，注意：32位和64位系统的区别，刚开始我64位的系统错选为32位的DevKit，导致后面安装时一直报错。
目前我选用的是Ruby 2.3.3 (x64)和DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe。
注意：ruby安装时可执行文件添加到环境变量中"Add Ruby executables to PATH"。或者自己在环境变量里配置。安装完成后可以使用Gitbash or cmd 输入ruby --version来查看。

devkit解压完后，如解压到D盘
`cd D:\DevKit
ruby dk.rb init
ruby dk.rb install`

**5.安装Octopress **
`cd d:\GitHub
git clone git://github.com/imathis/octopress.git octopress
cd octopress`

安装依赖项
`gem install bundler`
`bundle install`
安装octopress默认主题
`rake install`
`rake preview`

之后在浏览器里输入127.0.0.1:4000就可以观看效果了

途中遇到的问题：
1.添加国内淘宝gem源失败   
使用命令 gem sources -a https://ruby.taobao.org/

提示以下信息：
`Error fetching https://ruby.taobao.org/:
        SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed `
 修改方法:
 建议使用ruby-china的gem源，这个ruby-china的原来维护淘宝的gems的都不在淘宝了，现在搞了一个 `https://gems.ruby-china.org/` ，重新添加后数据正常。
 
 未完待续。。。


  [1]: http://www.yebangyu.org/blog/2015/10/17/howtoinstalloctopress/
  [2]: https://www.bbsmax.com/A/B0zq2DoXJv/
  [3]: http://blog.florianwolters.de/educational/2014/04/18/Running_Jekyll_with_GitHub_Pages_using_Windows_8.1_x64_and_Ruby_2.0_x64/
  [4]: http://stormzhang.com/other/2012/11/21/use-octopress-to-write-blog/
