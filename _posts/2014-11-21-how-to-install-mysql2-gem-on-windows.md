---
layout: post
title:  "在 Windows 7 64位下安装 mysql2 gem"
date:   2014-11-21 15:35:20
categories: ruby
---

在 Windows 下搭建 Ruby on Rails 开发环境最头痛的就是 native gem，尤其是每次安装 mysql2 都要折腾好久。
今天将 Ruby 升级到 2.1 之后又是一番折腾，主要是因为这个[BUG](https://bugs.ruby-lang.org/issues/8591)造成的。

环境：Windows 7 64位、[Ruby 2.1 64位](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.1.5-x64.exe?direct)、[DevKit 64位](http://cdn.rubyinstaller.org/archives/devkits/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)、[MySQL Connector/C 64位](http://cdn.mysql.com/Downloads/Connector-C/mysql-connector-c-6.1.5-winx64.zip)、[Structure svm map](https://structure-svm-map.googlecode.com/files/svm-map-win.zip)

+ 安装好 Ruby 及 DevKit；
+ 下载 MySQL Connector/C，解压到 D 盘；
+ 下载Structure svm map，然后将 svm-map-win\svm-map\python-mingw-lib 目录下的 gendef.exe 拷贝到 D:\mysql-connector-c-6.1.5-winx64\lib；
>执行如下命令生成 libmysql.def 文件；
{% highlight bat linenos %}
D:\mysql-connector-c-6.1.5-winx64\lib>gendef.exe libmysql.dll
{% endhighlight %}
+ 利用 mingw 中的 dlltool.exe 重新生成兼容 mingw64-gcc 的 limysql.lib 文件（注意：此步骤中的 libmysql.dll 必须处于 D:\mysql-connector-c-6.1.5-winx64\lib 目录，不能单独拷贝出来生成）；
{% highlight bat linenos %}
D:\mysql-connector-c-6.1.5-winx64\lib>D:\Ruby21\DevKit\mingw\bin\dlltool.exe -v --dllname libmysql.dll --def libmysql.def --output-lib libmysql.lib
{% endhighlight %}
+ 安装 mysql2.gem
{% highlight bat linenos %}
D:\>gem install mysql2 --platform=ruby -- '--with-mysql-lib="D:/mysql-connector-c-6.1.5-winx64/lib" --with-mysql-include="D:/mysql-connector-c-6.1.5-winx64/include"'
{% endhighlight %}
