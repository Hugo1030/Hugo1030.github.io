---
layout: post
title: "GitHub基本操作"
excerpt: "GitHub基本操作."
categories: tech
tags: [GitHub]
author: 沥川
modified:
---

### 安装GIT

1. 在[GIT官网](https://git-scm.com/)下载最新for MAC版本的GIT

2. 初始设置：
    * git config --global user.name "XXX"
    * git config --global user.email "xxx@gmail.com"
3. 提高命令输出的可读性，为你大部分输出加上颜色
    * git config --global color.ui auto

### 设置SSH Key

1. 创建SSH Key
    * ssh-keygen -t rsa -C "XXX@gmail.com"
    * id_rsa文件是私有密钥，id_rsa.pub是公开密钥
    * cat ~/.ssh/id_rsa.pub

2. 添加公开密钥
    * setting SSH and GPG keys
    * New SSh key复制粘贴就行

3. 用私人密钥与GitHub进行认证
    * ssh -T git@github.com

### clone已有仓库
1. 复制SSH clone URL
2. git clone URL
3. cd 仓库名称

### 提交
1. 修改文件
* cd Writer004 #进入仓库
* cd ch0 #进入ch0文件夹
2. git add 文件名.md #提交到暂存区
3. git commit -m "提示" #提交到仓库
4. git push #到远程仓库

### GitHub修改后复制到本地
1. 在GitHub上修改文件
2. git pull #直接复制修改到本地仓库
