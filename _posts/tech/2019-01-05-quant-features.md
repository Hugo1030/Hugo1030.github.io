---
layout: post
title: " TwoSigma: Quant features testing "
excerpt: " kaggle "
categories: tech
tags: [蟒营]
author: 沥川
modified:
---
## 背景

触发 [Any ideas for reaching the 0.7 tier?](https://www.kaggle.com/c/two-sigma-financial-news/discussion/75585) 

其中, @VadimNareyko (4th in this Competition) 特别提到

```
...
4. Use sample data to test the code before real training.
5. Train/Validation sets are really important - try to think how you validate your model.
6. Try more features and their combinations.
...
```

由于需要在测试集做 history_df, 目前线上测试一版需要 `5h+`, 由于本次测试一版只需要 `10m`

故需要尽可能在本地多做测试, 调好成绩后再 'submission'

## 计划

测试尽可能多的 quant features, 包含他们的组合..

## 方案

- [x] Moving average
- [x] Exponential Moving Average
- [x] MACD
- [x] Bollinger Band
- [x] RSI
- [x] Volume moving avreage

## 参考

- [Simple quant features using python](https://www.kaggle.com/youhanlee/simple-quant-features-using-python)
- [Use Python to calculate the Sharpe ratio for a portfolio](https://towardsdatascience.com/calculating-sharpe-ratio-with-python-755dcb346805)
- [Sharpe Ratio](https://www.investopedia.com/terms/s/sharperatio.asp)
- [Any ideas for reaching the 0.7 tier?](https://www.kaggle.com/c/two-sigma-financial-news/discussion/75585) 
- [Probability calibration for boosted trees](https://towardsdatascience.com/probability-calibration-for-boosted-trees-24cbd0f0ccae)

## Moving average

> An example of two moving average curves In statistics, a moving average (rolling average or running average) is a calculation to analyze data points by creating series of averages of different subsets of the full data set. It is also called a moving mean (MM)[1] or rolling mean and is a type of finite impulse response filter.

参考. [Moving_average Wiki Pedia](https://en.wikipedia.org/wiki/Moving_average)

- [x] 使用 3, 7, 14 lag + 4 features
    - valid loss1: 0.624249 / valid loss2: 0.641404
    - valid score: 1.50522 / test score: 0.70758
    
- [x] 使用 3, 7 lag + 4 features
    - valid loss1: 0.664212 / valid loss2: 0.658955
    - valid score: 1.10837 / test score: ?

- [x] 使用 3, 7, 14, 20 lag + 4 features ==> +++
    - valid loss1: 0.607309 / valid loss2: 0.615001
    - valid score: 1.71867 / test score: 0.71918

- [x] 使用 3, 7, 14, 20 lg + 3 features - open
    - valid loss1: 0.61068 / valid loss2: 0.619538
    - valid score: 1.65060 / test score: ? 

- [x] close_and_volume
    - valid loss1: 0.60487 / valid loss2: 0.617808
    - valid score: 1.70805 / test score: ? 

- [x] 修正 -1 后, 使用 3, 7, 14, 20 lag + 4 features
    - valid loss1: 0.60594 / valid loss2: 0.618462
    - valid score: 1.69276 / test score: 

- [x] add std
    - valid loss1: 0.61125 / valid loss2: 0.622347
    - valid score: 1.65302 / test score: ?

- [x] 3,5,7,14,20 lag
    - valid loss1: 0.60631 / valid loss2: 0.619793
    - valid score: 1.66843 / test score: ?

- [x] 3,5,7,14,20 lag - round 400 450
    - valid loss1: 0.586921 / valid loss2: 0.614442
    - valid score: 1.77644 / test score: 0.71397

- [x] 使用 3, 7, 14, 20 lag - round 500 500
    - valid loss1: 0.586921 / valid loss2: 0.614442
    - valid score: 1.77644 / test score: ?

## EMA (Exponential Moving Average)

参考 [Exponential_moving_average]( https://en.wikipedia.org/wiki/Moving_average#Exponential_moving_average)

- [x] ewma span = 4
    - valid loss1: 0.599245 / valid loss2: 0.611142
    - valid score: 1.72453 / test score: ?

- [x] ewma span = 7
    - valid loss1: 0.624249 / valid loss2: 0.641404
    - valid score: 1.50522 / test score: 0.70758

- [x] ewma span = 14
    - valid loss1: 0.624249 / valid loss2: 0.641404
    - valid score: 1.50522 / test score: 0.70758

- [x] ewma span = 20
    - valid loss1: 0.624249 / valid loss2: 0.641404
    - valid score: 1.50522 / test score: 0.70758

## MACD

MACD: (12-day EMA - 26-day EMA)

> Moving average convergence divergence (MACD) is a trend-following momentum indicator that shows the relationship between two moving averages of prices. The MACD is calculated by subtracting the 26-day exponential moving average (EMA) from the 12-day EMA

参考 [Moving Average Convergence Divergence - MACD]( https://www.investopedia.com/terms/m/macd.asp)

- [x] MACD
    - valid loss1: 0.589887 / valid loss2: 0.600827
    - valid score: 1.73427 / test score: 0.66297

## Bollinger Band

> Bollinger Bands are a type of statistical chart characterizing the prices and volatility over time of a financial instrument or commodity, using a formulaic method propounded by John Bollinger in the 1980s. Financial traders employ these charts as a methodical tool to inform trading decisions, control automated trading systems, or as a component of technical analysis. Bollinger Bands display a graphical band (the envelope maximum and minimum of moving averages, similar to Keltner or Donchian channels) and volatility (expressed by the width of the envelope) in one two-dimensional chart.

参考: [Bollinger_Bands](https://en.wikipedia.org/wiki/Bollinger_Bands)

- [x] rolling = 7
    - valid loss1: 0.588953 / valid loss2: 0.601884
    - valid score: 1.82173 / test score: 0.67890 (而且有很多 0)

- [x] rolling = 14
    - valid loss1: 0.589887 / valid loss2: 0.57906
    - valid score: 1.875077 / test score: ?

- [x] rolling = 20
    - valid loss1: 0.573969 / valid loss2: 0.588355
    - valid score: 1.870755 / test score: ?

## RSI

> The Relative Strength Index (RSI), developed by J. Welles Wilder, is a momentum oscillator that measures the speed and change of price movements. The RSI oscillates between zero and 100. Traditionally the RSI is considered overbought when above 70 and oversold when below 30. Signals can be generated by looking for divergences and failure swings. RSI can also be used to identify the general trend.

参考 [RSI Wiki Pedia](https://www.fidelity.com/learning-center/trading-investing/technical-analysis/technical-indicator-guide/RSI)

-  [x] rsi = 6
    + valid loss1: 0.600206 / valid loss2: 0.610734
    + valid score: 1.75754 / test score: 0.68932

-  [x] rsi = 6,14,20
    + valid loss1: 0.593609 / valid loss2: 0.602936
    + valid score: 1.77826 / test score: 0.64867

## Volume moving avreage

> A Volume Moving Average is the simplest volume-based technical indicator. Similar to a price moving average, a VMA is an average volume of a security (stock), commodity, index or exchange over a selected period of time. Volume Moving Averages are used in charts and in technical analysis to smooth and describe a volume trend by filtering short term spikes and gaps.

参考 [volume_ma](https://www.marketvolume.com/analysis/volume_ma.asp)

-  [x] rolling = 7
    + valid loss1: 0.607408 / valid loss2: 0.618092
    + valid score: 1.7038715 / test score: ?

-  [x] rolling = 7,14
    + valid loss1: 0.606649 / valid loss2: 0.617411
    + valid score: 1.71001 / test score: ?

-  [x] rolling = 7,14,20
    + valid loss1: 0.610523 / valid loss2: 0.616152
    + valid score: 1.66330 / test score: ?

## Changelog

- 2019-01-05 lichuan init.
