---
layout: post
title: " slack 频道接收 gitlab 提醒 "
excerpt: " slack 频道接收 gitlab 提醒 "
categories: tech
tags: [怼周会]
author: 沥川
modified:
---

## 背景

在 slack 接收 gitlab/github 提示信息由来已久, 长期未能亲自配置. 借由这次参加 two_sigma 竞赛, 在最后阶段, 为了让队友之间迅速 get 到进展情况, 故尝试之~

## 目标

slack 中 #kaggle2018 频道接收 gitlab 提示信息, 包括 issues/project/wiki ...

## 方案

- [x] 快速浏览 gitlab 文档, 找到 API 接口
- [x] 浏览 Slack 文档, 找到接收接口
- [x] 完成 #kaggle2018 接收提醒配置

## 追踪

- [3d [TASK] slack 频道如何接收 gitlab 提醒 #569](https://github.com/DebugUself/du4proto/issues/569)

## 记录

### slack 配置

- 浏览 gitlab 官方文档, 找到 [Slack Notifications Service](https://docs.gitlab.com/ee/user/project/integrations/slack.html) , 按步骤

1. Sign in to your Slack team and start a new [Incoming WebHooks configuration](https://debuguself.slack.com/apps/new/A0F7XDUAZ-incoming-webhooks).

2. 选择需添加的频道 #kaggle2018 

![](https://pics.ibrainbaby.cn/2018-12-29-071651.png)

3. 复制 Webhook URL，我们将在稍后的 GitLab 配置中使用它

![](https://pics.ibrainbaby.cn/2018-12-29-072114.png)


### gitlab 配置

1. 找到项目 Project > Settings > Integrations.
2. 选择 Slack notifications
3. 选择 Active 启动服务
4. 选择需要提醒的事件
5. 粘贴  Webhook URL 
6. 填写 usernage == Gitlab
7. 保存 change 即可

![](https://pics.ibrainbaby.cn/2018-12-29-072754.png)

- kaggle2018 频道测试成功 

![](https://pics.ibrainbaby.cn/2018-12-29-073121.png)

> ps. 官方文档才是正义!

## Changelog

- 181229 lichuan init. 0.5h


