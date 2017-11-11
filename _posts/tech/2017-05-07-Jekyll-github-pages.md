---
layout: post
title: "用Jekyll创建GitHub Pages个人博客"
excerpt: "用Jekyll创建GitHub Pages个人博客."
categories: tech
tags: [GitHub]
author: 沥川
modified:
---

### 一、GitHub Pages创建个人网站
1. 在GitHub上新建一个仓库，仓库名为uername.github.io
2. 克隆到本地仓库.
`git clone git@github.com:username/username.github.io.git`
3. `cd username.github.io`进入本地仓库
4. 创建一个简单的index.html文件测试一下
5. 将index.html文件上传到github上
6. 在chrome输入username.github.io，就可以初步看到效果了

### 二、Jekyll本地环境搭建
>[jekyll中文指导手册](http://jekyllcn.com/)

>[jekyll官网](https://jekyllrb.com/)

GitHub Pages为了提供对HTML内容的支持，选择了Jekyll作为模板系统，Jekyll是一个强大的静态模板系统，作为个人博客使用，基本上可以满足要求，也能保持管理的方便。

1. 安装ruby `brew install ruby`
2. 安装RubyGems
3. 利用Gem安装jekyll
`sodu gem install jekyll`
4. 安装bundle `sudo gem install bundle`
5. 下载满意的模板到本地仓库。
[Jekkyll Themes](http://jekyllthemes.org/)
6. 在本地仓库下，开启Jekyll环境`bundle exec jekyll serve`
7. 在浏览器输入http://127.0.0.1:4000/，即可看见本地博客了
7. 从本地git上传到GitHub `git push`
8. 在浏览器输入`username.github.io`就可以看到成果了

### 三、主题细节修改
1. 修改个人信息：博客名，描述等都在`_config.yml`
2. 修改背景图片：assets->image，直接替换文件，不过文件名要保持一致
3. 写文章：用Jekyll写博客，一篇文章就是一个文件，所有需要发表的文章都要放在_posts文件夹里。文件的命名要按YYYY-MM-DD-文章标题。后缀使用.md。
4. 书写格式，每篇文章的开头信息需要根据YAML格式写在两行三虚线之间。
  * layout: post
  * title: 这个是标题
  * date: 2017-05-07 22:20:24.000000000 +09:00
  * tags: Jekyll Github
