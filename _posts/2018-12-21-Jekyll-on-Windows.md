---
layout: post
title:  "Jekyll的安装使用以及遇到的一些问题"
date:   2017-12-21 17:31:01 +0800
categories: jekyll
tag: jekyll
---

* content
{:toc}


为了安装Jekyll，首先需要安装ruby的一套工具

## 1. ruby
在网站 https://rubyinstaller.org/downloads/ 中，下载ruby，这里需要注意的是，网站只提供了适用于Ruby2.0~3.0的Devkit
下载安装
查看是否安装成功
```
C:\Users\zhao kangkang>ruby -v
ruby 2.2.6p396 (2016-11-15 revision 56800) [x64-mingw32]
```
## 2. Devkit
下载解压，然后进入目录

```
C:\Users\zhao kangkang>cd C:\DevKit     #进入目录
C:\DevKit>ruby dk.rb init               #初始化
```
在config.yml中添加
```
C:/Ruby22-x64
```
继续执行以下命令
```
ruby dk.rb review  # 审查（非必须）
ruby dk.rb install  # 安装
gem -v  # 查看gem是否正常安装
```

## 3. jekyll
直接使用
```
gem install jekyll
```
提示版本错误，截至20181221，Jekyll官网上的版本已经到了3.8，需要更高版本
的ruby，可是2.3以上的ruby没有配套devkit，所以我选择安装低版本Jekyll

```
gem install jekyll -v 3.5
```
安装成功
## 4. 运行
进入目录，运行服务器
```
cd C:\Users\zhao kangkang\Documents\GitHub\zhaokangkang0572.github.io
jekyll serve
```

reference:
https://blog.csdn.net/mouday/article/details/79300135
