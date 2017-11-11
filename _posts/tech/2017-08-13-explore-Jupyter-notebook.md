---
layout: post
title: "探索Jupyter notebook"
excerpt: "自己探索Jupyter notebook记录"
categories: tech
tags: [Python]
author: 沥川
modified:
---

# 探索Jupyter notebook

## Jupyter notebook是什么？

Jupyther notebook 是一个可以把代码、图像、注释、公式和作图集于一处，从而实现可读性分析的一种灵活的工具。 **它的核心在于展示与快速迭代。**

![Jupyter notebook界面](https://www.dataquest.io/blog/images/jupyter/interface-screenshot.png)

## 为什么要使用 Jupyter notebook？

看看各路大神，都用Jupyter notebook干了什么，自然就回答了这个问题。

* 先来个有趣的，三体问题模拟器
    * [Three-Body Problem](http://nbviewer.jupyter.org/github/pjpmarques/Julia-Modeling-the-World/blob/master/Three-Body%20Problem.ipynb)
* 各路大神写的Python教程
    * [Introduction to Python](http://nbviewer.jupyter.org/github/ehmatthes/intro_programming/blob/master/notebooks/index.ipynb)
    * [Exploratory computing with Python by Mark Bakker](http://mbakker7.github.io/exploratory_computing_with_python/)
    * [Extended Introduction to Computer Science with Python](http://nbviewer.jupyter.org/github/yoavram/CS1001.py/tree/master/)
* 机器学习人工神经网络模型
    * [Neural Networks](http://nbviewer.jupyter.org/github/masinoa/machine_learning/blob/master/04_Neural_Networks.ipynb)
* 表格数据处理库Pandas教程
    * [.Analysing structured data using pandas](http://nbviewer.jupyter.org/github/phelps-sg/python-bigdata/blob/master/src/main/ipynb/pandas.ipynb)
* 大规模并行计算框架Spark教程
    * [Map-Reduce and Apache Spark](http://nbviewer.jupyter.org/github/phelps-sg/python-bigdata/blob/master/src/main/ipynb/spark-mapreduce.ipynb)
* Microsoft Office+Python自动化
    * [Automating Microsoft Office with Python](http://nbviewer.jupyter.org/github/sanand0/ipython-notebooks/blob/master/Office.ipynb)
* Twitter数据挖掘入门
    * [Datamining Twitter with tweepy](http://nbviewer.jupyter.org/github/hugadams/twitter_play/blob/master/tweepy_tutorial.ipynb)

## 如何安装Jupyter notebook？

* 直接安装[Anaconda](https://www.continuum.io/downloads)(强烈推荐)
* 使用pip安装Jupyter notebook
    * 在命令行输入：`pip3 install jupyter`

## 如何在Jupyter notebook内，实现Python2 and 3 共存？

### 安装Python 3.6

从官网下载Python 3.6对应的的Anaconda For macOS安装包——[Download](https://www.continuum.io/downloads#macos)。安装过程不赘述。

### 安装Python 2.7

打开terminal，输入

```conda create --name python27 python=2.7```

### 进入进入名为 env_name 的环境

`source activate env_name`

### 退出当前环境

`source deactivate`

### 显示所有环境

`conda env list`

## Jupyter notebook常用快捷键

使用快捷键可以大幅提高效率，让你欲罢不能。使用Cmd + Shift + P 调出命令面板。

Jupyter Notebook 有两种键盘输入模式。编辑模式，允许你往单元中键入代码或文本；这时的单元框线是绿色的。命令模式，键盘输入运行程序命令；这时的单元框线是灰色


### 命令模式 (按键 Esc 开启)

* Enter : 转入编辑模式
* Shift-Enter : 运行本单元，选中下个单元
* command-Enter : 运行本单元
* Alt-Enter : 运行本单元，在其下插入新单元
* Y : 单元转入代码状态
* M :单元转入markdown状态
* Up : 选中上方单元
* K : 选中上方单元
* Down : 选中下方单元
* J : 选中下方单元
* Shift-K : 扩大选中上方单元
* Shift-J : 扩大选中下方单元
* A : 在上方插入新单元
* B : 在下方插入新单元
* X : 剪切选中的单元
* C : 复制选中的单元
* F 在代码中查找、替换
* Shift-V : 粘贴到上方单元
* V : 粘贴到下方单元
* Z : 恢复删除的最后一个单元
* D,D : 删除选中的单元
* Shift-M : 合并选中的单元
* command-S : 文件存盘


### 编辑模式 ( Enter 键启动)
* Tab : 代码补全或缩进
* command-A : 全选
* command-Z : 复原
* command-Up : 跳到单元开头
* command-End : 跳到单元末尾
* command-Left : 跳到左边一个字首
* command-Right : 跳到右边一个字首
* Shift-Enter : 运行本单元，选中下一单元
* command-Enter : 运行本单元
* Alt-Enter : 运行本单元，在下面插入一单元

## 轻松链接到文档

在库、方法或变量的前面打上?，即可打开相关语法的帮助文档。

```
?str.replace

Docstring: L.append(object) -> None -- append object to end
Type:      method_descriptor
```

```
?list.pop

Docstring:
L.pop([index]) -> item -- remove and return item at index (default last).
Raises IndexError if list is empty or index is out of range.
Type:      method_descriptor
```

```
?dict.get

Docstring: D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None.
Type:      method_descriptor
```

## 在Jupyter notebook里面作图

推荐使用matplotlib，可通过%matplotlib inline 激活
```
from pylab import *
from mpl_toolkits.mplot3d import Axes3D

fig = figure()
ax = Axes3D(fig)
X = np.arange(-4, 4, 0.25)
Y = np.arange(-4, 4, 0.25)
X, Y = np.meshgrid(X, Y)
R = np.sqrt(X**2 + Y**2)
Z = np.sin(R)

ax.plot_surface(X, Y, Z, rstride=1, cstride=1, cmap='hot')

show()
```

## Jupyter Magic命令

Jupyter notebook提供了许多魔法命令，使得在Jupyter notebook环境中的操作更加得心应手。魔法命令都以%或者%%开头，以%开头的成为行命令，%%开头的称为单元命令。行命令只对命令所在的行有效，而单元命令则必须出现在单元的第一行，对整个单元的代码进行处理。

执行%magic可以查看关于各个命令的说明，而在命令之后添加?可以查看该命令的详细说明。

推荐阅读Jupyter magic命令的[相关文档](http://ipython.readthedocs.io/en/stable/interactive/magics.html)，它一定会对你很有帮助。

下面是我最爱的几个：

### Jupyter Magic - %run: 运行python代码

%run 可以运行.py格式的python代码——这是众所周知的。不那么为人知晓的事实是它也可以运行其它的jupyter notebook文件，这一点很有用。
```
%run ./ex1.py
```
### Jupyter Magic - %who: 列出所有的全局变量
```
one = "for the money"
two = "for the show"
three = "to get ready now go cat go"
%who str
```
### Jupyter Magic – 计时

有两种用于计时的jupyter magic命令： %%time 和 %timeit.当你有一些很耗时的代码，想要查清楚问题出在哪时，这两个命令非常给力。

%%time 会告诉你cell内代码的单次运行时间信息。

```
%%time
a = []
for i in range(10000000):
    a.append(i)
```

%%timeit 使用了Python的 timeit 模块，该模块运行某语句100，000次（默认值），然后提供最快的3次的平均值作为结果。

```
%%timeit
a = []
for i in range(10):
    a.append(i)
```

### 在notebook内用不同的内核运行代码

如果你想要，其实可以把不同内核的代码结合到一个notebook里运行。

只需在每个单元格的起始，用Jupyter magics调用kernal的名称：

* %%bash
* %%HTML
* %%python2
* %%python3
* %%ruby
* %%perl

```
%%bash
        for i in {1..5}
        do
           echo "i is $i"
        done
```

## 展示你的Jupyter notebook

* GitHub 天然支持 Jupyter Notebook —— 上传笔记后，你可以直接在仓库中看到渲染效果，管理版本。[展示文档](https://github.com/Hugo1030/learnpython/blob/master/jupyter-notebook-turials.ipynb)
* 可以使用官方的[nbviewer](https://nbviewer.jupyter.org/)，也非常容易展示和分享，比如[展示文档](http://nbviewer.jupyter.org/github/Hugo1030/learnpython/blob/master/jupyter-notebook-turials.ipynb)

## Changelog
170813 沥川创建，博文Jupyter notebook版本链接[jupyter文档地址](https://github.com/Hugo1030/learnpython/blob/master/jupyter-notebook-turials.ipynb)
