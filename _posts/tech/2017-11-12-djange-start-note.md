---
layout: post
title: "《Django 入门与实践》"
excerpt: "《Django 入门与实践》笔记"
categories: tech
tags: [Django]
author: 沥川
modified:
---

# Django 入门与实践

## 课程介绍

### 课程目标
* 学习并掌握 Django 的基本用法
* 了解 Django 的部分原理以及各组件的含义
* 可以独立使用 Django 进行基本的网站开发

### 课程内容
* 了解 Django
* 搭建开发环境
* 完成一个简单的个人博客网站

### 课程知识要求
* 掌握 Python 语言
* 了解 HTML 语言
* 了解浏览器上网的基本原理

---

## 课前准备

### Django 简介
* Django 是一个基于 Python 的高级 Web 开发框架
* 它能够让开发人员进行高效且快速的开发
* 高度集成（不用自己造轮子），免费并且开源

## 创建项目目录下部分文件的作用
### 创建步骤
* 打开命令行，进入想要安置项目的目录
* 命令行输入：django-admin startproject myblog
* 若没有报错，则创建项目成功

### 项目目录结构
* manage.py
* myblog
    * __init__.py
    * settings.py
    * urls.py
    * wsgi.py

#### manage.py
* 与项目进行交互的命令行工具集的入口
* 项目管理器
* 执行 python manage.py 来查看所有命令

#### myblog目录
* 项目的一个容器
* 包含项目最基本的一些配置
* 目录名称不建议修改

#### wsgi.py
* WSGI (Python Web Server Gateway Interface)
* 中文名：Python 服务器网关借口
* Python 应用与 Web 服务器之间的接口

#### urls.py
* url 配置文件
* Django 项目中所有地址（页面）都需要我们自己去配置其URL

#### settings.py
* 项目的总配置文件
* 里面包含了数据库、Web 应用、时间等各种配置

#### __init__.py
* Python 中声明模块的文件
* 内容默认为空

---

## 创建应用
### 创建步骤
* 打开命令行，进入项目中 manage.py 同级目录
* 命令行输入：python manage.py startapp blog
* 添加应用名到 settings.py 中的 INSTALLED_APPS 里

### 目录结构
* migrations
  * __init__.py
* __init__.py
* admin.py
* apps.py
* models.py
* tests.py
* views.py

#### migrations
* 数据移植（迁移）模块
* 全部自动生成

#### admin.py
* 该应用的后台管理系统配置

#### app.py
* 该应用的一些配置

#### models.py
* 数据模块
* 使用 ORM 框架
* 类似于 MVC 结构中的 Models（模型）

#### test.py
* 自动化测试模块
* Django 提供了自动化测试功能
* 在这里编写测试脚本（语句）

#### views.py
* 执行响应的代码所在模块
* 代码逻辑处理的主要地点
* 项目中大部分代码均在这里编写

### 创建第一个页面（响应）
* 编辑 blog.views
  * 每个响应对应一个函数，函数必须返回一个响应
  * 函数必须存在一个参数，一般约定为request
  * 每一个响应（函数）对应一个 URL
* 编辑 urls.py
  * 每个 URL 都以 url 的形式写出来
  * url 函数放在 urlpatterns 列表中
  * url 函数三个参数：URL（正则），对应方法，名称

---

## 第一个 Templates

### 第二种 URL 配置
* 包含其他 URL
  * 在根 urls.py 中引入 include
  * 在 APP 目录下创建 urls.py 文件，格式与根 urls.py 相同
  * 根 urls.py 中 url 函数第二个参数改为 include('blog.urls')
* 注意事项
  * 根 urls.py 针对 APP 配置的 URL 名称，是该 APP 所有 URL 的总路径
  * 配置 URL 时注意正则表达式结尾符号 $ 和 /

### Templates 介绍
* 什么是 Templates
  * HTML 文件
  * 使用了 Django 模板语言（Django Template Language, DTL）
  * 可以使用第三方模板（如Jinja2）

### 开发第一个 Template
* 步骤
  * 在 APP 的根目录下创建名叫 Templates 的目录
  * 在该目录下创建 HTML 文件
  * 在 views.py 中返回 render()
* DTL 初步使用
  * render() 函数中支持一个 dict 类型参数
  * 该字典是后台传递到模板的参数，键为参数名
  * 在模板中使用 {{ 参数名 }} 来直接使用
* Django 查找 Template
  * Django 按照 INSTALLED_APPS 中添加顺序查找 Templates
  * 不同 APP 下 Templates 目录中的同名.html 文件会造成冲突  (重点问题)
* 解决 Templates 冲突方案
  * 在 APP 的 Templates 目录下创建以 APP 名为名称的目录
  * 将 html 文件放入新创建的目录下
  * 注意修改 views.py 文件中的 render 参数

---
## Models

### Modesl 介绍
* Django 中的 Models 是什么？
  * 通常，一个 Models 对应数据库的一张数据表
  * Django 中 Models 以类的形式表现
  * 它包含了一些基本字段以及数据的一些行为
* ORM
  * 对象关系映射（Object Relation Mapping）
  * 实现了对象和数据之间的映射
  * 影藏了数据访问的细节，不需要编写 SQL 语句

### 编写 Models
* 步骤
  * 在应用根目录下创建 models.py，并引入 models 模块
  * 创建类，继承 models.Model，该类即是一张数据表
  * 在类中创建字段
* 字段创建
  * 字段即类里面的属性（变量）
  * attr = models.CharField(max_lenth=64)
  * 查看官方网站文档，字段的可选参数

### 生成数据表
* 步骤
  * 命令行进入 manage.py 同级目录
  * 执行 python3 manage.py makemigrations app名（可选）
  * 再执行 python3 manage.py migrate
* 查看
  * Django 会自动在 app/migrations/ 目录下生成移植文件
  * 执行 python3 manage.py sqlmigrate 应用名 文件id 查看 SQL 语句
  * 默认 sqlite3 的数据库在项目根目录下 db.sqlite3
* 查看并编辑 db.sqlite3
  * 使用第三方软件
  * SQlite Expert Personal
  * 轻量级，完全免费

### 页面呈现数据
* 后台步骤
  * views.py 中 import models
  * article = models.Article.objects.get(pk=1) # 这里的 pk 指的是「主键」
  * render(request,page,{'article':article})
* 前端步骤
  * 模板可直接使用对象以及对象的"."操作
  * {{ article.title }}

---
## Admin

### Admin 简介
* 什么是 Admin ?
  * Admin 是 Django 自带的一个功能强大的自动化数据管理界面
  * 被授权的用户可直接在 Admin 中管理数据库
  * Django 提供了许多针对 Admin 的定制功能

### 配置 Admin
* 创建用户
  * python3 manage.py createsuperuser 创建超级用户
  * localhost:8000/admin/ Admin 入口
  * 修改 settings.py 中 LANGUAGE_CODE = 'zh_Hans'
* 配置应用
  * 在应用下 admin.py 中引入自身的 models 模块（或里面的模型类）
  * 编辑 admin.py : admin.site.register(models.Article)
* 修改数据
  * 点击 Article 超链接进入 Article 列表页面
  * 点击任意一条数据，进入编辑页面修改
  * 编辑页面下方一排按钮可执行相应操作

### 修改数据默认显示名称
* 步骤
  * 在 Article 类下添加一个方法
  * 根据 Python 版本 .3 选择__str__(self) 或 .2 选择 __unicode__(self)
  * return self.title

---

## 完善博客
### 博客页面设计
* 页面概要
  * 博客主页面
  * 博客文章内容页面
  * 博客撰写页面
* 主页面内容
  * 文章标题列表，超链接
  * 发表博客按钮（超链接）
* 列表编写思路
  * 取出数据库中所有文章对象
  * 将文章对象们打包成列表，传递到前端
  * 前端页面把文章以标题超链接的形式逐个列出
* 模板 for 循环
  * {% for xx in xxs %}
  * HTML 语句
  * {% endfor %}

### 博客文章页面
* 页面内容
  * 标题
  * 文章内容
  * 修改文章按钮（超链接）
* URL 的参数传递
  * 参数写在响应函数中 request 后，可以有默认值
  * URL 正则表达式：r'^article/(?P<article_id>[0-9]+)/$
  * URL 正则中的组名必须和参数名一致

### Django 中的超链接
* 超链接目标地址
  * href 后面是目标地址
  * template 中可以用 "{% url 'app_name:url_name' param %}"
  * 其中 app_name 和 url_name 都在 url 中配置

### 再配 URL
* url 函数的名称参数
  * 根 urls，卸载 include() 的第二个参数位置， namespace='blog'
  * 应用下则写在 url() 的第三个参数位置，name='artcle'
  * 主要取决于是否使用 include 引用了另一个 url 配置文件

### 博客撰写页面
* 页面内容
  * 标题编辑栏
  * 文章内容编辑区域
  * 提交按钮
* 编辑响应函数
  * 使用 request.POST['参数名']获取表单数据
  * models.Article.objects.create(title, content)创建对象

### 两个编辑页面
* 思路
  * 新文章为空，修改文章有内容
  * 修改文章页面有文章对象
  * 文章的 ID
* 修改数据
  * article.title = title
  * article.save()

---

## 补充内容

### Templates 过滤器

* 什么是过滤器？
  * 卸载模板中，属于 Django 模板语言
  * 可以修改模板中的变量，从而显示不同的内容
* 怎么使用过滤器？
  * {{ value | filter }}
  * 例子: {{ list_nums | length }}
  * 过滤器可叠加：{{ value | filter1 | filter2 | ...}}
* 更多 Django 过滤器内容看官网

### Django Shell
* 什么是 Django Shell?
  * 它是一个 Python 的交互式命令行程序
  * 它自动引入了我们的项目环境
  * 我们可以使用它与我们的项目进行交互
* 如何使用 Django Shell?
  * python manage.py shell
  * from blog.models import Article
  * Article.objects.all()
* 有什么用？
  * 我们可以使用 Django shell 来进行一些调试工作
  * 测试未知的方法

### Admin
* 创建 admin 配置类
  * class ArticleAdmin(admin.ModelAdmin)
  * 注册：admin.site.register(Article, ArticleAdmin)
* 显示其他字段
  * list_display = ('title', 'content')
  * list_display 同时支持 tuple 和 list
* 过滤器
  * list_filter = ('pub_time', )
* 更多信息参考官方文档

---
## 课程回顾
* 课程介绍
  * 学习目标及内容
  * 课程基础知识要求
* 课前准备
  * 介绍 Django
  * 课程基础知识要求
  * 介绍 Django
  * 通过浏览器浏览网页的基本原理
* 开发环境搭建
* 创建项目及应用
  * 创建项目
  * 创建应用
  * 创建（响应）页面
* 第一个 Template
  * 重新配置 URL
  * 介绍 Templates
  * 开发第一个 Template
* Models
  * 介绍 Models
  * 编写博客的 Model
  * 将数据呈现在页面上
* Admin
  * 创建超级用户
  * 配置 Admin
  * 使用 Admin 修改数据库
* 完善博客
  * 博客主页面
  * 博客内容页面
  * 博客编写页面
* 补充内容
  * Templates 过滤器
  * Django shell
  * Admin 增强
