---
layout: post
title:  "在 Windows 7 64位下安装 mysql2 gem"
date:   2014-11-21 15:35:20
categories: ruby gem
---

在 Windows 下搭建 Ruby on Rails 开发环境最头痛的就是 native gem，尤其是每次安装 mysql2 都要折腾好久。
今天将 Ruby 升级到 2.1 之后发现之前的 mysql2 gem 安装方法已经无效，经过坚持不懈的努力终于安装成功，特此记录以加强记忆。

之前的安装环境：Windows 7 64bit、Ruby 2.0、DevKit、MySQL Connector/C 32bit，然后执行下述命令就OK了
{% highlight bat %}
D:\>gem install mysql2 --platform=ruby -- '--with-mysql-lib="D:\mysql-connector\lib" --with-mysql-include="D:\mysql-connector\include"'
{% endhighlight %}
换到 Ruby 2.1 以后怎么都不能通过编译，经过无数次的尝试终于找到可行的方法
环境：Windows 7 64bit、[Ruby 2.1](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.1.5-x64.exe?direct)、[DevKit](http://cdn.rubyinstaller.org/archives/devkits/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)、MySQL 5.6 x64
{% highlight bat %}
D:\>gem install mysql2 --platform=ruby -- '--with-mysql-dir="D:\MySQL"'
{% endhighlight %}
