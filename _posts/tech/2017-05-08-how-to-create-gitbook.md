---
layout: post
title: "Gitbook简易配置手册"
excerpt: "Gitbook简易配置手册."
categories: tech
tags: [GitHub]
author: 沥川
modified:
---

1. 登录Gitbook，可以使用GitHub账号登录
2. 创建Gitbook，点击+New新建一本书，在类型里面选择GitHub,然后选择要关联的仓库
3. GtiHub安装集成选择，settings->Installed integrations->Repository access选择All repositories
4. 在GitHub关联的仓库中，新增SUMMRY.md文件，这个文件作用是在Gitbook中新增目录
5. SUMMRY.md文件的写法是，[]里面是章节名称，()里面是链接。
  * [Part I](part1/README.md)
      * [Writing is nice](part1/writing.md)
      * [GitBook is nice](part1/gitbook.md)
  * [Part II](part2/README.md)
      * [We love feedback](part2/feedback_please.md)
      * [Better tools for authors](part2/better_tools.md)
6. 点入Gitbook选择Read按钮就可以观看了。
7. 全部都可以在本地Git上操作，上传到GitHub，然后自动关联到Gitbook非常方便。
