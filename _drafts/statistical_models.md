---
layout: post
title: 统计模型概要
categories:
- Data Science
---

# 指数分布

在概率论和数理统计中，指数分布是一种概率分布，描述了泊松过程中事件之间的时间间隔，泊松过程中的事件以一个恒定平均比率发生。指数分布是伽马分布的一个特例，是几何分布的连续模拟，其关键特性是无记忆。除了被用于泊松过程的分析之外，还在多种其他情况下被发现。   
指数分布用于对一段时间内事件发生之间的时间间隔，或者是空间内事件的距离建模。例如：

+ 在一场世界杯足球比赛中多次进球间的时间间隔
+ 一个帮助中心里用户打进电话的时间间隔
+ 不同的直径大于1米的流星撞击地球的时间间隔
+ 一台机器连续宕机的时间间隔
+ 癌症转移病人从确诊到死亡的时间
+ 管道中连续中断的距离

若如下条件为真，则指数分布是适当的模型：

+ $$ X $$是事件键的时间（或距离），且$$ X > 0 $$。
+ 一件事件的发生并不影响下一个事件发生的概率，即事件的发生是独立的。
+ 事件发生的比率是恒定的，位于某个区间内。
+ 两个事件不可能在完全相同的时刻发生。

如果这些条件为真，则$$ X $$是一个指数随机变量，其分布为指数分布。指数分布由单个参数$$ \lambda $$决定。$$ \lambda $$为事件比率，是每个单位时间内事件的总数。概率密度函数为：

$$
f(x) = \lambda e^{-\lambda x}
$$

累加分布函数，即事件发生间隔小于某个特定间隔$$ x $$的概率如下：

$$
P(\text{time between events is} \le\ x)=1-e^{-\lambda x}
$$

两个函数的示意图绘制代码如下：
{% highlight python %}
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd


n = 5000
xcor = np.linspace(0, 5, n)
lbd = [0.5, 1, 1.5]
color = ['orange', 'purple', 'lightblue']
pdf = pd.DataFrame()
cdf = pd.DataFrame()
for m in lbd:
    label = '$ \lambda = $' + str(m)
    expo = np.exp((-m) * xcor)
    pdf[label] = expo * m
    cdf[label] = 1 - expo
pdf.plot(xcor, color=color, linewidth=2)
plt.xlabel(r'$ X $')
plt.ylabel(r'$ P(x) $')
cdf.plot(xcor, color=color, linewidth=2)
plt.xlabel(r'$ X $')
plt.ylabel(r'$ P(x) $')
plt.show()
{% endhighlight %}

![指数分布概率密度函数图]({{site.url}}/assets/images/data_science/exponential_dist_pdf.png)
![指数分布累加概率函数图]({{site.url}}/assets/images/data_science/exponential_dist_cdf.png)
参考资料：[维基百科](https://en.wikipedia.org/wiki/Exponential_distribution)

# 威布尔分布

威布尔分布是一个连续概率分布。一个威布尔随机变量的概率密度函数为：

$$
f(x;\lambda,k) =
\begin{cases}
\frac{k}{\lambda}\left(\frac{x}{\lambda}\right)^{k-1}e^{-(x/\lambda)^k} & x\geq0,\\
0 & x\lt0,
\end{cases}
$$

这里$$ k > 0 $$是分布的形状参数，而$$ \lambda > 0 $$是尺度参数。如果$$ X $$的数量是“失效时间”，则威布尔分布确定了失效率（故障率）与时间的某个幂成正比。形状参数$$ k $$为该幂指数加1，如此参数能有如下解释：

+ $$ k < 1 $$意味着失效率随着时间下降。这说明存在很高的早期故障率，次品将会在早期被淘汰。
+ $$ k = 1 $$意味着失效率恒定，不随时间变化。这可能显示有随机外来事件导致死亡或失效。威布尔分布降低到指数分布。
+ $$ k > 1 $$意味着失效率随着时间增加。这可能是因为存在“老化”过程。

[注释]: <> (还有新产品渗透理论，如果以后需要，可以再看)

威布尔分布的累加分布函数为：

$$
F(x;k,\lambda) =
\begin{cases}
1 - e^{-(x/\lambda)^k} & x \geq 0 \\
0 & x < 0
\end{cases}
$$

绘制函数图的代码如下：

{% highlight python %}
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt


# m为lambda值
n, m = 2500, 1
# 不从0开始，是为了避免后面出现“divide by zero in power”的警告。
xcor = np.linspace(1e-8, 2.5, n)
pdf = pd.DataFrame()
cdf = pd.DataFrame()
k_value = [0.5, 1, 1.5, 5]
for k in k_value:
    label = '$ \lambda = 1, k = $' + str(k)
    expo = -np.power(xcor / m, k)
    expo = np.exp(expo)
    pdf[label] = (k / m) * np.power(xcor / m, k - 1) * expo
    cdf[label] = 1 - expo
pdf.plot(xcor)
plt.ylim([0, 2.5])
cdf.plot(xcor)
plt.show()
{% endhighlight %}

![指数分布概率密度函数图]({{site.url}}/assets/images/data_science/weibull_distribution_pdf.png)
![指数分布累加概率函数图]({{site.url}}/assets/images/data_science/weibull_distribution_cdf.png)
参考资料：[维基百科](https://en.wikipedia.org/wiki/Weibull_distribution)

# 二项分布

具有参数$$ n $$和$$ p $$的二项分布是一个离散概率分布，表示的是在$$ n $$个以$$ p $$为概率成功独立实验事件的序列中，成功的次数。

## 概率质量函数

一般而言，若随机变量$$ X $$遵循参数$$ n \in \mathbb{N} $$和$$ p \in [0,1] $$的二项分布，则记为$$ X ~ B(n,p) $$。在$$ n $$次尝试中准确地获得$$ k $$次成功的概率由以下概率密度函数给定：

$$
f(k;n,p) = Pr(X=k)=\binom{n}{k}p^k(1-p)^{n-k}
$$

这里$$ \binom{n}{k}=\frac{n!}{k!(n-k)!}, k = 0, 1, 2, ..., n $$是二项式系数，也是该分布名称的由来。

## 累加分布函数

累加分布函数可表示如下：

$$
F(k;n,p) = Pr(X \leq k) = \displaystyle\sum_{i=0}^{\lfloor k \rfloor}\binom{n}{k}p^i(1-p)^{n-i}
$$

据[NumPy](https://docs.scipy.org/doc/numpy/reference/generated/numpy.random.binomial.html)上所说，在利用随机取样对一个种群估算比例的标准误差时，正态分布工作良好的前提是$$ n \times p > 5 $$，否则应该使用二项分布。

函数图形绘制代码如下：
{% highlight python %}
import numpy as np
import matplotlib.pyplot as plt
from scipy.misc import comb


list_n = [20, 20, 40]
list_p = [0.5, 0.7, 0.5]
colors = 'bry'

fig, axes = plt.subplots(2, 1, sharex=True)
plt.xlim([-3, 43])

for n, p, c in zip(list_n, list_p, colors):
    x = np.arange(0, n + 1)
    pmf = comb(n, x) * np.power(p, x) * np.power(1 - p, n - x)
    cdf = np.cumsum(pmf)
    label = 'p = ' + str(p) + ', n = ' + str(n)
    axes[0].scatter(x, pmf, label=label, c=c, alpha=0.5)
    axes[1].scatter(x, cdf, label=label, c=c, alpha=0.5)

axes[0].legend()
axes[1].legend(loc='lower right')
plt.show()
{% endhighlight %}

![二项分布函数图]({{site.url}}/assets/images/data_science/binomial_dist.png)
参考资料：[维基百科](https://en.wikipedia.org/wiki/Binomial_distribution)


# 泊松分布

泊松分布是一种离散概率分布，表达了给定数量的事件在一个固定的时间（和/或空间）间隔内发生的概率，如果这些事件的发生自上次事件的发生是独立的、有已知的平均发生比率。泊松分布还能用于其他类型间隔内事件发生次数，如距离、面积或体积。
当有大量的独立稀少事件时，对发生的事件计数。   
举例：基因突变、在特定十字路口的交通事故、某收件箱中的邮件（数量）   
均值=方差   

## 假想：泊松分布在何时为一个恰当的模型？

泊松分布在以下假设为真时是一个恰当模型：

+ K是间隔内一种事件发生的次数且K能取值0, 1, 2, ...
+ 一起事件的发生不影响下一起事件发生的概率。即，事件都独立发生。
+ 事件发生的比例是恒定地位于特定区间内。
+ 两起事件不能在相同的时刻发生。
+ 事件发生的概率和间隔的长度成正比。

如果以上条件为真，则K是一个泊松随机变量，其分布为泊松分布。

## 泊松分布的事件概率

$$
P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}, k=0,1,2,...
$$

这里$$ \lambda $$是单位间隔内事件发生的平均次数，是正实数，且有
$$
\lambda=\operatorname{E}(X)=\operatorname{Var}(X)
$$
作为无偏差的估计函数并非很有意义的例子：泊松分布，其原理还要仔细领会。

参考资料：[维基百科](https://en.wikipedia.org/wiki/Poisson_distribution)
