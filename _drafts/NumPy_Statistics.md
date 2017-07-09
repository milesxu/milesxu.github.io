layout: post
title: NumPy 统计学函数库示例
categories:
- Data Science
- NumPy
---

# `numpy.percentile`

针对给定数组和比例，计算一个插值。   
重要参数有数组`a`，百分率`q`，插值方法`interpolation`。   
给定一个长度为`N`的向量`V`，`V`的第`q`百分率是`V`的有序拷贝中$$ q/100 $$的分位点所在的位置。如果各元素规范化后的排名不能够准确地匹配`q`值，则由最近的两个邻居的值和距离以及插值方法共同决定返回值。`q`的元素取值范围$$ [0,100] $$，`q`为50则该函数相对于计算中点，`q`为0和100则分别相对于求最小值和最大值。   
插值方法有线性'linear'、较小值'lower'、较大值'higher'、最近'nearest'、中点'midpoint'。默认是线性。

# `numpy.std`

沿着指定的轴计算标准偏差。标准偏差是一个分布的散布。   
标准偏差是各元素到平均值的均方差的平均值的平方根：`std = sqrt(mean(abs(x - x.mean())**2))`   
随机变量、统计学种群、数据集、或者概率分布是他们的方差的平方根。

## 离散随机变量

当$$ X $$从有限数据集$$ x_1, x_2, ..., x_N $$中获得随机值，获得每个值的概率一样，则标准偏差是

$$
\sigma = \sqrt{\frac{1}{N}[(x_1-\mu)^2 + (x_2-\mu)^2 + \dots + (x_N-\mu)^2]}, \qquad\text{where}\quad \mu = \frac{1}{N}(x_1+\dots+x_N),
$$

或使用求和符号

$$
\sigma = \sqrt{\frac{1}{N}\displaystyle\sum_{i=1}^{N}(x_i-\mu)^2}, \qquad \text{where}\quad \mu = \frac{1}{N}\displaystyle\sum_{i=1}^{N}x_i.
$$

又或者获取每个值的概率互相不同，设得到$$ x_1 $$的概率是$$ p_1 $$,得到$$ x_2 $$的概率是$$ p_2 $$, ...,得到$$ x_N $$的概率是$$ p_N $$。此时标准偏差为

$$
\sigma = \sqrt{\displaystyle\sum_{i=1}^{N}p_i(x_i-\mu)^2}, \qquad \text{where} \quad \mu=\displaystyle\sum_{i=1}^{N}p_ix_i.
$$

参考资料：[维基百科](https://en.wikipedia.org/wiki/Standard_deviation)

# `numpy.var`

沿着指定的轴计算方差，返回数组元素的方差，一个对分布的散布的度量。   
方差是到均值的偏差的平方的平均，即`var = mean(abs(x - x.mean())**2)`
