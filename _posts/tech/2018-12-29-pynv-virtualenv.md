---
layout: post
title: " 使用 pyenv 和 pyenv-virtualenv 配置虚拟环境 "
excerpt: " 使用 pyenv 和 pyenv-virtualenv 配置虚拟环境 "
categories: tech
tags: [怼周会]
author: 沥川
modified:
---

## 背景

触发 [Pythonic 101 Ch00](https://gitlab.com/101camp/py/blob/master/ch00.md)

需要配置运行环境

- Python 2.7.15
- zhpy 模块

## 目标

- 尝试使用 pyenv + pyenv-virtualenv 高速合理的建立/删除 工程运行环境

## 计划

  - [x] 安装 pyenv
  - [x] 安装 pyenv-virtualenv 插件
  - [x]  pyenv 安装 Python 2.7.15
  - [x] 配置 2.7.15 虚拟环境
  - [x] pip install zhpy 模块

## 尝试

### setp1 

- 使用 pyenv 安装 Python 2.7.15

输入 `$pyenv versions`

返回

```
system
* 3.6.1 (set by /Users/hugo/.pyenv/version)
```

说明已经安装 pyenv

然后输入 `$ pyenv install 2.7.15`

报错 

```
python-build: definition not found: 2.7.15

See all available versions with `pyenv install --list'.

If the version you need is missing, try upgrading pyenv:

  brew update && brew upgrade pyenv
``` 

输入 `brew upgrade pyenv` 来升级 pyenv

升级后 `$ pyenv install -l` 发现 2.7.15 版本出现

再次输入 `$ pyenv install 2.7.15` 完成

## step2

- 配置虚拟环境 

```
$ pyenv virtualenv 2.7.10 env-2.7.10
```

报错

```
pyenv: no such command `virtualenv'
```

- 原来缺少 virtualenv 插件, 搜索安装 并创建虚拟环境

```
git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv
$ pyenv virtualenv 2.7.15 env-2.7.15
```
- 激活时

```
pyenv activate virtualenvs env-2.7.15
```

报错

```
Failed to activate virtualenv.

Perhaps pyenv-virtualenv has not been loaded into your shell properly.
Please restart current shell and try again.
```

重启 shell 试试, 仍然报错

通过查看资料, 发现是 pyenv 和 pyenv-virtualenv 未加入环境变量, 所以

```
$ echo 'eval "$(pyenv init -)"' >> ~/.zshrc
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
$ exec $SHELL
$ source ~/.zshrc
```
即可启用

### 常用命令

pyenv命令集:

    pyenv install --list
    
        查询所有可以安装的版本
        
    pyenv install 2.7.14
        
        安装所需的版本
        
    pyenv uninstall
    
        卸载特定的Python版本。

    pyenv version
    
        显示当前活动的Python版本
        
    pyenv global 2.7.14
    
        Python的全局设置，整个系统生效
        
    pyenv global 2.7.14
    
        Python的局部设置，当前目录生效
        
    pyenv local --unset
    
        取消设置    

    更多参考GitHub...

pyenv-virtualenv命令集:

    pyenv virtualenv 2.7.14 venv2714

        制定版本创建virtualenv
        
    pyenv virtualenvs
        
        列出现有virtualenvs
    
    pyenv activate virtualenv的名称
    
        激活pyenv virtualenv
        
    pyenv deactivate
    
        停用pyenv virtualenv

    pyenv uninstall my-virtual-env
    
        删除现有virtualenv

## 参考

- [Mac安装pyenv和pyenv-virtualenv](https://www.jianshu.com/p/13e300c63abd)
- [使用 pyenv 管理 Python 版本 ](http://einverne.github.io/post/2017/04/pyenv.html)
- [Mac端pycharm平台下pyenv和pyenv-virtualenv管理python版本的安装和简单实用](https://blog.csdn.net/lilihan12358/article/details/78636742)
- [pyenv/pyenv: Simple Python version management](https://github.com/pyenv/pyenv)


## changelog
- 2018-12-29 lichuan init. explore pyenv 1h


