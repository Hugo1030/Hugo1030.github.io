---
layout: post
title: "Leture 1: The Learning Problem"
excerpt: "Learning From Data note, leture 1"
categories: tech
tags: [Deep Learning]
author: 沥川
modified:
---

## The learning problem - Outline
* Example of machine learning
* Components of Learning
* A simple model
* Types of learning
* Puzzle

## Example: Predicting how a viewer will rate a movie

* 10% improvement = 1 million dollar prize, 这是机器学习的商业价值, 一点小小的调优, 可以更合理的分配资源, 提升效率, 得到巨大经济利益.
* The essence of machine learning:
    * A pattern exists. 机器学习如果要成立, 模式/规律必须存在, 完全随机无学习可言
    * We cannot pin it down mathematically. 人类无法找到数学规律, 需要借助计算机强大的计算能力, 和模式识别能力, 来帮助人类找到模型.
    * We have data on it. 机器学习其实是从数据中学习, 或者转化成数字, 进行处理.

## Movie rating - a solution
* viewer: like movies? / like action? / prefers blockbusters?... likes Tom Cruise?
* movie: comedy content / action content / blockbusters? ... Tom Cruise in it?
* 结合 viewer 和 movie 的特征, 建立学习算法, 得到评价分数

## Components of learning
* Formalization:
    * Input: X (customer application)
    * Output: y (good/bad customer?)
    * Target function: f: X -> y (ideal credit approval formula)
    * Data: $(x_1, y_1), (x_2, y_2), ... , (x_n, y_n)$ (historical records)
    * Hypothesis: g: X -> y (formula to be used)

