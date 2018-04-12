---
layout: post
title: "[Stacked Hourglass Networks for Human Pose Estimation] 论文笔记"
excerpt: "[Stacked Hourglass Networks for Human Pose Estimation] 论文笔记"
categories: tech
tags: [Deep Learning]
author: 沥川
modified:
---

[Stacked Hourglass Networks for Human Pose Estimation](https://arxiv.org/abs/1603.06937), 在单人姿态估计上的表现亮眼, 与我们的比赛更加接近

## Abstract

- 重复使用自下而上 / 自上而下, 结合 中间监督
- 关键词 Human Pose Estimation

## Introduction

- 理解图片或视频人类的行为, 一个关键是姿势预测
- 在动画和人机交互领域起到重要作用
- 一个好的姿态预测系统需要在闭包/变形/遮挡, 还有在衣服和光线变化下具有鲁棒性
- 卷积神经网络取代过去手工或者图形合成方法, 有了巨大的进步
- 将多个低分辨率的模型进行结合
    
## Related Work
- 汤姆森等人算法的关键是卷积网络和图形模型联合使用
- 图形模型学习关节间典型的空间关系
- 我们没有使用任何图形模型或任何显式的人体建模, 便获得了卓越的性能

## Network Architecture

### Hourglass Design

- 沙漏的设计是因为需要在每一个尺度上捕捉信息
- 神经网络需要有一些机制是的进程有效且固定特征
- 我们使用一个带有跳过层的管道来保存每个分辨率的空间信息
- 沙漏建立的步骤
    - 利用卷积和最大池化层得到一个非常低的分辨率图像
    - 到达最低分辨率后, 通过上采样的方发和原图进行合并
    - 沙漏的结构是对称的, 所以每次下降都有一个向上
    - 到达输出分辨率后, 连续两个 1×1 卷积用于生成最终的网络预测
    - 网络的输出是一组热力图

### Layer Implementation

- 我们使用一些其他网络模型如残差学习模型和"Inception" 替换后, 效果进一步提升
- 其他的方法并未得到进一步提升
- 最后扩展了残差模型(residual modules)
- 没有使用超过 3×3 以上的 filter
- 图像需要处理成 256x256
- 最终输出 256 个特征

### Stacked Hourglass with Intermediate Supervision (中间监督)

- 通过堆叠的方式, 让模型自底向上和自顶向下反复预测图像机制
- 这种方法的关键, 是中间的热力图上我们可以应用损失预测
- 每个沙漏后都会产生一个预测, 然后这个预测会在本地和全局进行展示
- 然后下面的沙漏会再次处理这些高阶特征, 然后输出更多的高阶特征
- 多次迭代和中间监督
- 如果想理解整体姿势含义, 独立关键点是没用的, 还需要知道他们之间的联系
- 反复的 top-down, bottom-up 可以缓解这个问题
- 上一个阶段的结果, 作为输入传递到下一个阶段
- 不同阶段对整体理解不同层面
- 这种方法在不同范围内向后和向前很重要, 因为是最终输出是所有关键点的结合
- 最终的模型使用了 8 组 hourglass
- 值得注意的是, 这些 hourglass 并不共享权重
- 但是使用同一个真实预测作为损失函数

### Training Details

- 我们在两个基准(benchmark) 数据集上测试 FLIC 和 MPII 测试了我们的模型
- 我们将所有图片处理成 256x256
- 数据增强 旋转(+-30°) 缩放(+-0.25)
- 我们避免了平移增强, 因为目标任务的位置是决定谁应该被网络注释的关键线索
- 使用 torch7 , 优化器选择 rmsprop, 学习率 2.5e-4
- 当精度没有下降后, 将学习率下降了 5 倍
- 使用了 batch 归一化, 来提升训练
- 在输出最后结果时, 将原始输入和反转版本结合, 得到平均热力图, 效果提升 1%
- 使用均方差 (MSE) 作为损失函数, 由预测 和 2D高斯中点组成

## Results

### Evaluation

- 评估指标使用 PCK (Percentage of Correct Keypoints)
- 所谓 PCK 就是误差范围除以一个固定距离, 比如头部尺寸

### Ablation Experiments

- 我们主要有两个设计: Hourglass 的堆叠和中间监督的影响
- 最后发现堆叠加上中间监督的效果最好

## Further Analysis

### Multiple People

- 在多人情景中, 我们以中心和范围来确定某人
- 容易出现混淆情况
- 单人效果较好, 多人注释超出了这个工作的范围

### Occlusion

- 阻塞性能评估容易失败有两个原因
    - 第一是关节不可见, 但是给出了位置
    - 第二是关节的位置不出现, 比如只出现上半身, 非全身
- 不可见和遮挡会影响模型的效果
- 遮挡是一个显著的挑战
- 使用热力图可以有效提升遮挡情况下的表现

## Conclusion

- 说明了 hourglass/ Intermediate supervision / stacked 在模型表现中的作用
- 在多人和遮挡情况下, 仍有不错的表现

## Changelog
* 18.4.12 init.

