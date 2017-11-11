---
layout: post
title: "吴恩达《神经网络和深度学习》课程笔记（3）-- 神经网络基础之Python与向量化"
excerpt: "神经网络基础之Python与向量化"
categories: tech
tags: [deeplearning]
author: 沥川
modified:
---
上节课我们主要介绍了逻辑回归，以输出概率的形式来处理二分类问题。我们介绍了逻辑回归的Cost function表达式，并使用梯度下降算法来计算最小化Cost function时对应的参数w和b。通过计算图的方式来讲述了神经网络的正向传播和反向传播两个过程。本节课我们将来探讨Python和向量化的相关知识。

### 1. Vectorization
深度学习算法中，数据量很大，在程序中应该尽量减少使用loop循环语句，而可以使用向量运算来提高程序运行速度。

向量化（Vectorization）就是利用矩阵运算的思想，大大提高运算速度。例如下面所示在Python中使用向量化要比使用循环计算速度快得多。

```
import numpy as np
import time

a = np.random.rand(1000000)
b = np.random.rand(1000000)

tic = time.time()
c = np.dot(a,b)
toc = time.time()

print(c)
print("Vectorized version:" + str(1000*(toc-tic)) + "ms")

c = 0
tic = time.time()
for i in range(1000000):
	c += a[i]*b[i]
toc = time.time()

print(c)
print("for loop:" + str(1000*(toc-tic)) + "ms")
```

输出结果类似于：
```
250031.204952
Vectorized version:1.09100341796875ms
250031.204952
for loop:482.65600204467773ms
```

从程序运行结果上来看，该例子使用for循环运行时间是使用向量运算运行时间的约300倍。因此，深度学习算法中，使用向量化矩阵运算的效率要高得多。

为了加快深度学习神经网络运算速度，可以使用比CPU运算能力更强大的GPU。事实上，GPU和CPU都有并行指令（parallelization instructions），称为Single Instruction Multiple Data（SIMD）。SIMD是单指令多数据流，能够复制多个操作数，并把它们打包在大型寄存器的一组指令集。SIMD能够大大提高程序运行速度，例如python的numpy库中的内建函数（built-in function）就是使用了SIMD指令。相比而言，GPU的SIMD要比CPU更强大一些。

![](https://pic1.zhimg.com/v2-29f79857ebf4c76becffea83279b0bcc_b.png)

### 2. More Vectorization Examples
上一部分我们讲了应该尽量避免使用for循环而使用向量化矩阵运算。在python的numpy库中，我们通常使用np.dot()函数来进行矩阵运算。下面两张图是向量化的例子：

![](https://pic3.zhimg.com/v2-11795964ce7245aae1b9a7e2d6c1928e_b.png)

我们将向量化的思想使用在逻辑回归算法上，尽可能减少for循环，而只使用矩阵运算。值得注意的是，算法最顶层的迭代训练的for循环是不能替换的。而每次迭代过程对J，dw，b的计算是可以直接使用矩阵运算。

![](https://pic1.zhimg.com/v2-f272c74c747ca085470884048f54e978_b.png)

### 3. Vectorizing Logistic Regression
在《神经网络与深度学习》课程笔记（2）中我们介绍过，整个训练样本构成的输入矩阵X的维度是（ n_x  ，m），权重矩阵w的维度是（ n_x ，1），b是一个常数值，而整个训练样本构成的输出矩阵Y的维度为（1，m）。利用向量化的思想，所有m个样本的线性输出Z可以用矩阵表示：

![](http://www.zhihu.com/equation?tex=Z%3Dw%5ETX%2Bb)

在python的numpy库中可以表示为：

```
Z = np.dot(w.T,X) + b
A = sigmoid(Z)
```

其中，w.T表示w的转置。

![](https://pic3.zhimg.com/v2-e59de020e6f5523e37a9f2ef78aab8ba_b.png)

这样，我们就能够使用向量化矩阵运算代替for循环，对所有m个样本同时运算，大大提高了运算速度。

### 4. Vectorizing Logistic Regression’s Gradient Output
再来看逻辑回归中的梯度下降算法如何转化为向量化的矩阵形式。对于所有m个样本，dZ的维度是（1，m），可表示为：

![](http://www.zhihu.com/equation?tex=dZ%3DA-Y)

db可表示为：

![](http://www.zhihu.com/equation?tex=db%3D%5Cfrac1m+%5Csum_%7Bi%3D1%7D%5Emdz%5E%7B%28i%29%7D)

对应的程序为：
```
db = 1/m*np.sum(dZ)
```

dw可表示为：

![](http://www.zhihu.com/equation?tex=dw%3D%5Cfrac1m+X%5Ccdot+dZ%5ET)

对应的程序为：

```
dw = 1/m*np.dot(X,dZ.T)
```

![](https://pic2.zhimg.com/v2-321093e317292067dadc9f254eba2b15_b.png)

这样，我们把整个逻辑回归中的for循环尽可能用矩阵运算代替，对于单次迭代，梯度下降算法流程如下所示：

```
Z = np.dot(w.T,X) + b
A = sigmoid(Z)
dZ = A-Y
dw = 1/m*np.dot(X,dZ.T)
db = 1/m*np.sum(dZ)

w = w - alpha*dw
b = b - alpha*db
```

其中，alpha是学习因子，决定w和b的更新速度。上述代码只是对单次训练更新而言的，外层还需要一个for循环，表示迭代次数。

![](https://pic4.zhimg.com/v2-9b75a3dc671b767e98d3475602db61fb_b.png)

### 5. Broadcasting in Python

下面介绍使用python的另一种技巧：广播（Broadcasting）。python中的广播机制可由下面四条表示：

* 让所有输入数组都向其中shape最长的数组看齐，shape中不足的部分都通过在前面加1补齐
* 输出数组的shape是输入数组shape的各个轴上的最大值
* 如果输入数组的某个轴和输出数组的对应轴的长度相同或者其长度为1时，这个数组能够用来计算，否则出错
* 当输入数组的某个轴的长度为1时，沿着此轴运算时都用此轴上的第一组值

简而言之，就是python中可以对不同维度的矩阵进行四则混合运算，但至少保证有一个维度是相同的。下面给出几个广播的例子，具体细节可参阅python的相关手册，这里就不赘述了。

![](https://pic4.zhimg.com/v2-ab58055ecc749f6493156d16b8691cf3_b.png)

![](https://pic4.zhimg.com/v2-7b41ac86f537bea2b1a8864cc63536c3_b.png)

![](https://pic4.zhimg.com/v2-1ca8d9a02a38a014847e55c234334b97_b.png)

值得一提的是，在python程序中为了保证矩阵运算正确，可以使用reshape()函数来对矩阵设定所需的维度。这是一个很好且有用的习惯。

### 6. A note on python/numpy vectors
接下来我们将总结一些python的小技巧，避免不必要的code bug。

python中，如果我们用下列语句来定义一个向量：

```
a = np.random.randn(5)
```

这条语句生成的a的维度是（5，）。它既不是行向量也不是列向量，我们把a叫做rank 1 array。这种定义会带来一些问题。例如我们对a进行转置，还是会得到a本身。所以，如果我们要定义（5，1）的列向量或者（1，5）的行向量，最好使用下来标准语句，避免使用rank 1 array。

```
a = np.random.randn(5,1)
b = np.random.randn(1,5)
```

除此之外，我们还可以使用assert语句对向量或数组的维度进行判断，例如
```
assert(a.shape == (5,1))
```

assert会对内嵌语句进行判断，即判断a的维度是不是（5，1）的。如果不是，则程序在此处停止。使用assert语句也是一种很好的习惯，能够帮助我们及时检查、发现语句是否正确。

另外，还可以使用reshape函数对数组设定所需的维度：
```
a.reshape((5,1))
```

![](https://pic1.zhimg.com/v2-46eead267bf45c47046ff66cdcc070f4_b.png)

### 7. Quick tour of Jupyter/iPython Notebooks

Jupyter notebook（又称IPython notebook）是一个交互式的笔记本，支持运行超过40种编程语言。本课程所有的编程练习题都将在Jupyter notebook上进行，使用的语言是python。

### 8. Explanation of logistic regression cost function(optional)
在上一节课的笔记中，我们介绍过逻辑回归的Cost function。接下来我们将简要解释这个Cost function是怎么来的。

首先，预测输出 \hat y 的表达式可以写成：

![](http://www.zhihu.com/equation?tex=hat+y%3D%5Csigma%28w%5ETx%2Bb%29)

其中， ![](http://www.zhihu.com/equation?tex=%5Csigma%28z%29%3D%5Cfrac%7B1%7D%7B1%2Bexp%28-z%29%7D)。 \hat y 可以看成是预测输出为正类（+1）的概率：

![](http://www.zhihu.com/equation?tex=%5Chat+y%3DP%28y%3D1%7Cx%29)

那么，当y=1时：

![](http://www.zhihu.com/equation?tex=p%28y%7Cx%29%3D%5Chat+y)

当y=0时：

![](http://www.zhihu.com/equation?tex=p%28y%7Cx%29%3D1-%5Chat+y)

我们把上面两个式子整合到一个式子中，得到：

![](http://www.zhihu.com/equation?tex=P%28y%7Cx%29%3D%5Chat+y%5Ey%281-%5Chat+y%29%5E%7B%281-y%29%7D)

由于log函数的单调性，可以对上式P(y|x)进行log处理：

![](http://www.zhihu.com/equation?tex=log%5C+P%28y%7Cx%29%3Dlog%5C+%5Chat+y%5Ey%281-%5Chat+y%29%5E%7B%281-y%29%7D%3Dy%5C+log%5C+%5Chat+y%2B%281-y%29log%281-%5Chat+y%29)

我们希望上述概率P(y|x)越大越好，对上式加上负号，则转化成了单个样本的Loss function，越小越好，也就得到了我们之前介绍的逻辑回归的Loss function形式。

![](http://www.zhihu.com/equation?tex=L%3D-%28y%5C+log%5C+%5Chat+y%2B%281-y%29log%281-%5Chat+y%29%29)

如果对于所有m个训练样本，假设样本之间是独立同分布的（iid），我们希望总的概率越大越好：

![](http://www.zhihu.com/equation?tex=max%5C+%5Cprod_%7Bi%3D1%7D%5Em%5C+P%28y%5E%7B%28i%29%7D%7Cx%5E%7B%28i%29%7D%29)

同样引入log函数，加上负号，将上式转化为Cost function：

![](http://www.zhihu.com/equation?tex=J%28w%2Cb%29%3D-%5Cfrac1m%5Csum_%7Bi%3D1%7D%5EmL%28%5Chat+y%5E%7B%28i%29%7D%2Cy%5E%7B%28i%29%7D%29%3D-+%5Cfrac1m%5Csum_%7Bi%3D1%7D%5Emy%5E%7B%28i%29%7D%5C+log%5C+%5Chat+y%5E%7B%28i%29%7D%2B%281-y%5E%7B%28i%29%7D%29log%281-%5Chat+y%5E%7B%28i%29%7D%29)

上式中， \frac1m 表示对所有m个样本的Cost function求平均，是缩放因子。

### 9. Summary
本节课我们主要介绍了神经网络基础——python和向量化。在深度学习程序中，使用向量化和矩阵运算的方法能够大大提高运行速度，节省时间。以逻辑回归为例，我们将其算法流程包括梯度下降转换为向量化的形式。同时，我们也介绍了python的相关编程方法和技巧。

### 注明
文章中的内容大都来自Coursera上的课程材料

### Changelog
* 2017-09-24 创建
