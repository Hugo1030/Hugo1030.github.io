---
layout: post
title: "天池盐城乘用车量预测, 第 11 名解答思路"
excerpt: "天池盐城乘用车量预测, 第 11 名解答思路"
categories: tech
tags: [Deep Learning]
author: 沥川
modified:
---

## 整体赛题回顾

本次比赛, 是阿里天池举办的[印象盐城·数创未来大数据竞赛 - 乘用车零售量预测](https://tianchi.aliyun.com/competition/introduction.htm?spm=5176.100066.0.0.510bd780HWbxXh&raceId=231640)大数据竞赛, 与怼圈小伙伴大妈,阿虎和蔡俊组队, 最终取得第 11 名的成绩.

本次比赛中, 我负责整体策略设计, 特征工程和模型训练的工作.

初赛提供2012年1月-2017年10月盐城分车型销量配置数据,预测 2017 年 11 月和 12 月盐城分车型销量数据.

复赛数据量扩大, 提供2012年1月-2017年12月全国分城市分车型销量配置数据,全国整体车型产量数据,全国宏观经济月度数据. 分别预测 2018 年 1 月和 2 月全国分城市分车型销量数据.

下面主要以复赛算法为例来进行讲解.

**采用 RMSLE 作为评测指标:**

![][image-1]

相较于初赛的 RMSE, RMSLE 对大值误差不那么敏感, 但是对小值的偏差更加敏感.

比如: 1024 预测 2048, 误差绝对值很大, 但是 log 的平方只有 1. 但如果将 1 预测成 8, 误差绝对值很小, log 后的平方为 4, RMSLE 的误差是前者的 4 倍, 所以需要特别注意销量小的值.

## 解决方案概述

首先我们队数据集进行了清洗工作, 对缺值进行了均值填充, 对重复值和异常值, 进行了清洗去除等操作.

接着针对最要的销量表进行特征提取工作, 第一部分是与 class_id 相关, 例如: 品牌,厢数,排量...等特征, 代替 class_id 的对车型进行描述. 另一部分是关于时间与销量关系的时间序列特征.然后选用了部分宏观经济和产量指标作为特征辅助特征.

最后训练了 GBDT, XGBoost 两种模型, 并进行了加权融合.

## 数据集划分

- A 榜

    - 预测区间: 2018.01
    - 特征提取区间:
        - 2013.01 - 2017.11
        - 2013.02 - 2017.12

- B 榜

    - 预测区间: 2018.02
    - 特征提取区间:
        - 2012.01 - 2017.11
        - 2012.02 - 2017.12
        - 2013.01 - 2017.11
        - 2013.02 - 2017.12

## 特征工程

特征工程主要包含三大类, 分别是针对时间和销量相关的时间序列特征, 与车型相关的 class\_id 描述团, 还有与宏观及产量销量的特征.

以下简要地说明各部分特征:
- 时序相关特征
    - total\_sale\_last1M 分省市上月整体销量
    - total\_last12M\_sum 分省市上一年整体销量
    - sale\_last1M 上月销量
    - sale\_last12M 去年同月销量
    - cnt\_classid 本月有多少种车型在销售
    - year 年份
    - month 月份
    - how\_many\_month\_sale 已销售月累加
    - sale\_last2M/3M/6M/12M\_sum/std/avg/max/min 2/3/6/12个月时间窗口,的和/标准差/平均/最大/最小值
    - lastyear\_MoM 上一年同月环比
    - spring\_festival 是否包含春节
- 车型 class\_id 相关特征
    - 类别特征进行 one-hot 编码
        - brand\_id 品牌
        - compartment 箱数
        - type\_id 车型类别
        - level\_id 车型级别
        - department\_id 车型系别
        - gearbox\_type 变速器形式
        - if\_charging 是否增压
        - driven\_type\_id 驱动形式
        - fuel\_type\_id 燃料种类
        - newenergy\_type\_id 新能源类型
        - emission\_standards\_id 排放标准
        - if\_MPV\_id 是否微客
        - if\_luxurious\_id 是否豪华
    - 数值类型, 取平均值
        - displacement 排量
        - price\_level 成交段
        - power 功率
        - engine\_torque 发动机扭矩
        - car\_length 车长
        - car\_width 车宽
        - car\_height 车高
        - total\_quality 总质量
        - equipment\_quality 整备质量
        - rated\_passenger 额定载客
        - wheelbase 轴距
        - front\_track 前轮距
        - rear\_track 后轮距
- 整体宏观特征
    - oil\_price 油价
    - purchase\_tax 低排量购置税
- 产量特征
    - produce\_quantity\_last1m 上月同车型产量


## 模型设计与融合
将 A 榜排名第一(RMSLE = 0.79)的预测值, 填入 18.1 销量. 并提取 18.2 特征

训练了 XGBoost 和 GBDT 两个模型, 然后进行简单的加权融合, XGBoost × 0.4 + XGBoost × 0.6, 作为最终结果提交


## Changelog
* 2018-03-16 创建

