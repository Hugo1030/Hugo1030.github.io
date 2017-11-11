---
layout: post
title: "基于git+gollum的个人wiki管理器"
excerpt: "gollum的安装"
categories: tech
tags: [git]
author: 沥川
modified:
---

* 使用MacPorts package manager来安装gollum。[MacPorts地址](https://www.macports.org/)
* Macports安装成功后，加入环境：将/opt/local/bin和/opt/local/sbin添加到$PATH搜索路径中，编辑/etc/profile文件中，加上
```
export PATH=/opt/local/bin:$PATH
export PATH=/opt/local/sbin:$PATH
```
* `sudo port install ruby_select <ruby-portname>`安装ruby，已安装可跳过这步
* `sudo port select --set ruby <ruby-portname>`将已安装ruby设为默认
* `sudo port install icu`安装icu依赖包
* `sudo gem install charlock_holmes -- --with-icu-dir=/opt/local/lib/icu --with-opt-include=/opt/local/include/ --with-opt-lib=/opt/local/lib/`设定charlock_holmes标准目录
* `sudo gem install gollum`安装gollum
* `gollum --v`查看版本及是否安装成功。
* 建立一个wiki目录进行git管理
```
mkdir wiki
cd wiki
git init
gollum
```
* 在浏览器中访问`http://localhost:4567/`，就OK了
<img width="1044" alt="1" src="https://user-images.githubusercontent.com/24667603/29804416-09da9c22-8cb5-11e7-9812-44131f6b8067.png">

## Changelog
* 2017-08-29 创建
