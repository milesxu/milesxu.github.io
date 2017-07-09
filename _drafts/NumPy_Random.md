---
layout: post
title: NumPy 随机取样函数库示例
categories:
- Data Science
- NumPy
---

# `numpy.random.randn`

该函数返回一个标准正态分布的序列。如果参数是正整数，或者可以转换为正整数，`randn`生成和参数所代表的维度和形状相同的数组，其中的值随机浮点数，从均值为0、方差为1的一元正态分布序列中取样。   
根据[维基百科](https://en.wikipedia.org/wiki/Normal_distribution),正态分布的概率密度函数为：  

$$ f(x \; | \; \mu, \sigma^2) = \frac{1}{\sqrt{2\sigma^2\pi}} \; e^{-\frac{(x-\mu)^2}{2\sigma^2}} $$   

其中：  

- $$ \mu $$是该分布的均值或期望值
- $$ \sigma $$是标准偏差
- $$ \sigma^2 $$是方差

如果想得到特定分布$$ \mathcal{N}(\mu, \, \sigma^2) $$的随机取样，可用公式：   

$$ \sigma \times $$ `np.random.randn(...)` $$ + \mu $$   

[维基百科](https://en.wikipedia.org/wiki/Normal_distribution)上有不同均值、方差的分布函数示意图，可直接对上述公式求值然后画出来。而我们可以用直方图来验证利用`randn`方法获得的数据的分布情况。

{% highlight python %}
import numpy as np
import matplotlib.pyplot as plt


# 通过画直方图验证randn的数据分布。
n = 50000
arr = np.random.randn(n)
plt.hist(arr, bins=100)
plt.show()
{% endhighlight %}

结果图如下：
![正态分布柱状图]({{site.url}}/assets/images/numpy/randn_1.png)

通过`randn`获得的数据，可以构成类似维基上的累加分布函数图，但物理意义是否一样或者类似，笔者还未明了……代码如下：
{% highlight python %}
import numpy as np
import matplotlib.pyplot as plt


# 通过randn画概率累加图
n = 50000
arr = np.sort(np.random.randn(n))
ycor = np.linspace(0, 1, n)
plt.plot(arr, ycor, 'r', linewidth=2)
mu = [0, 0, -2]
sigma = [0.2, 5.0, 0.5]
color = ['b', 'y', 'g']
legend = ['$ \mu = $' + str(0) + ', ' + '$ \sigma^2 = $' + str(1.0)]
for m, s, c in zip(mu, sigma, color):
    xcor = np.sqrt(s) * arr + m
    plt.plot(xcor, ycor, c, linewidth=2)
    legend.append('$ \mu = $' + str(m) + ', ' + '$ \sigma^2 = $' + str(s))
plt.xlim([-5, 5])
plt.xlabel(r'$ X $')
plt.ylabel(r'$ \Phi_{\mu,\sigma^2}(x) $')
plt.legend(legend, loc='best')
plt.grid()
plt.show()
{% endhighlight %}
结果图如下：
![类似累加分布函数图]({{site.url}}/assets/images/numpy/randn_2.png)

另外，用pandas库的DataFrame来画与维基同样分布图的代码如下：
{% highlight python %}
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as tkr
import pandas as pd


def normal_dist(N, sig, mu):
    return lambda x: N/(sig*np.sqrt(2*np.pi)) * np.e**(-(x-mu)**2/(2 * sig**2))

n = 50000
x_series = pd.Series(np.linspace(-5, 5, n))
curves = pd.DataFrame()
mu = [0, 0, 0, -2]
sigma_square = [0.2, 1, 5, 0.5]
color = ['b', 'r', 'y', 'g']
for m, s in zip(mu, sigma_square):
    label = '$ \mu = $' + str(m) + ', ' + '$ \sigma^2 = $' + str(s)
    curves[label] = x_series.apply(normal_dist(1, np.sqrt(s), m))
curves.plot(x_series, color=color, grid=True, linewidth=2)
plt.ylim([-0.05, 1.05])
plt.xlim([-5.5, 5.5])
plt.xlabel(r'$ X $')
plt.ylabel(r'$ \Phi_{\mu,\sigma^2}(x) $')
ax = plt.axes()
ax.xaxis.set_major_locator(tkr.MultipleLocator(1))
ax.yaxis.set_major_locator(tkr.MultipleLocator(0.2))
ax.xaxis.set_minor_locator(tkr.MultipleLocator(.25))
ax.yaxis.set_minor_locator(tkr.MultipleLocator(.05))
plt.show()
{% endhighlight %}

![正态分布图]({{site.url}}/assets/images/numpy/normal_distribution.png)

# `numpy.random.choice`

对给定的1维数组生成一个随机采样。可以指定输出的数组形状，并且还可以指定被采样数组中每个元素的出现概率。如果未指定，则对所有元素按照均匀分布采样。被采样的数组元素可以是整数以外的类型，比如字符串。

# `numpy.random.uniform`

从一个均匀分布中取样。取样值是在参数给定的区间内均匀分布。均匀分布的概率密度函数为

$$
p(x) = \frac{1}{b-a}
$$

在区间$$ [a, b) $$内的任何地方，在其他地方取值均为0。
NumPy的很多函数都能指定输出数组形状，这点非常分布，比如这里可以一次性生成多次模拟需要用到的数组的集合。   
活用：如果要随机选择多次使用的数组索引，则可以对数组的`shape`进行`choice`操作，因为参数可以是一个正整数，然后在0到此整数间随机选择。
