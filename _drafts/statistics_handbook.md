layout: post
title: 统计学知识速查
categories:
- Data Science
- Statistics
---

# 核密度估计

核密度估计（KDE， kernel density estimation）是一种估计随机变量的 *概率密度函数* 的非参数方法。基于一个有限的数据取样，当关于种群的推断已经做出时，核密度估计是基础的数据平滑问题。   
设$$ (x_1, x_2, \dots, x_n) $$是从某个具有未知密度$$ f $$的分布中抽取的独立的、相同分布的样本。我们在意的是估计函数$$ f $$的形状。其核密度估计为：

$$
\hat{f}_h(x)=\frac{1}{n}\displaystyle\sum_{i=1}^{n}K_h(x-x_i)=\frac{1}{nh}\displaystyle\sum_{i=1}^{n}K\left(\frac{x-x_i}{h}\right)
$$

这里$$ K(\cdot) $$是一个核——一个非负函数，积分值为1，均值为0，而$$ h > 0 $$为平滑参数，称为带宽。有下标$$ h $$的核被称为伸缩核并被定义为$$ K_h(x) = \frac{1}{h}K(\frac{x}{h}) $$。   
常用的核函数包括：[Uniform, Triangular, Epanechnikov, Quartic, Trweight, Tricube, Gaussian, Cosine, Logistic, Sigmoid function, Silverman kernel, etc](https://en.wikipedia.org/wiki/Kernel_(statistics)#Kernel_functions_in_common_use)。   
seaborn库提供了[kdeplot](http://seaborn.pydata.org/generated/seaborn.kdeplot.html)函数，可用来进行估计并画图。

参考资料：[维基百科](https://en.wikipedia.org/wiki/Kernel_density_estimation)

# 相关性

pandas的`DataFrame`有[corr](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.corr.html)方法   
[matplotlib](http://matplotlib.org/api/pyplot_api.html#module-matplotlib.pyplot)有绘制[自相关](https://en.wikipedia.org/wiki/Autocorrelation)的函数`acorr`，以及[互相关](https://en.wikipedia.org/wiki/Cross-correlation)的函数`xcorr`。
参考资料：[维基百科](https://en.wikipedia.org/wiki/Correlation_and_dependence)

# 统计假设与检验

统计假设是一类可基于对某个过程的观察进行测试的假设，而该过程已经经由随机变量的集合建模。统计假设检验是统计推断的一种方法。与之关联的一个重要概念是[零假设](https://en.wikipedia.org/wiki/Null_hypothesis)   
通用校验统计学，要看。

参考资料：[维基百科](https://en.wikipedia.org/wiki/Statistical_hypothesis_testing)

# 偏差

一个估计函数的偏差或偏差函数是该估计函数的期望值和被估计的参数的真实值之间的差异。偏差为0的估计函数或决策规则称为公正的，否则就是有偏差的。   
偏差也能用中点来衡量，而不是均值（期望值），偏差和一致性有关，因为一致的估计函数会收敛，且渐进于0偏差（因此收敛到正确值），尽管在一致的序列里的单个估计函数可能是有偏差的。在使用一个有偏差的估计函数时，其偏差也会被估计。   
设一个统计模型，以实数$$ \theta $$为参数，使得观察获得的数据有概率分布$$ P_\theta(x)=P(x|\theta) $$。而一个基于任何观察数据$$ x $$的统计量$$ \hat{\theta} $$充当$$ \theta $$的估计函数。即我们假定我们的数据遵循未知的分布$$ P_\theta(x)=P(x|\theta) $$，并构造估计函数$$ \hat{\theta}，其将观察到的数据映射到我们希望的接近于$$ \theta $$的值。则该估计函数的偏差定义为

$$
\text{Bias}_\theta[\hat{\theta}] = E_\theta[\hat{\theta}]-\theta=E_\theta[\hat{\theta}-\theta]
$$

这里$$ E_\theta $$表示分布$$ P_\theta(x)=P(x|\theta) $$的期望值，即$$ x $$所有的可能的观察的平均。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/Bias_of_an_estimator)

# 期望值

一个随机变量的期望值，是经过长期大量重复试验所得值的平均。[大数定理](https://en.wikipedia.org/wiki/Law_of_large_numbers)陈述了在重复的次数接近无限时，这些值的算术平均值几乎必然收敛到期望值。又称期望、数学期望。   
一个离散随机变量的期望值是所有可能值的概率权重平均。对于连续随机变量，其期望值为其和概率密度函数相乘然后求积分。正式定义：一个随机变量的期望值是随机变量关于其[概率测度](https://en.wikipedia.org/wiki/Probability_measure)的积分。   

## 定义

### 一元离散随机变量，有限论域

设随机变量$$ X $$以概率$$ p_1 $$获得值$$ x_1 $$，以概率$$ p_2 $$获得值$$ x_2 $$，以此类推，直到$$ p_k $$获得值$$ x_k $$。则随机变量$$ X $$的期望定义为
$$
\operatorname{E}[X] = x_1p_1 + x_2p_2 + \dots + x_kp_k
$$
因为所有概率$$ p_i $$的总和为1（$$ p_1 + p_2 + \dots + p_k = 1 $$），期望值可以看做是[权重平均](https://en.wikipedia.org/wiki/Weighted_average)：
$$
\operatorname{E}[X]=\frac{x_1p_1+x_2p_2+\dots+x_kp_k}{1}=\frac{x_1p_1+x_2p_2+\dots+x_kp_k}{p_1+p_2+\dots+p+k}
$$
TODO：掷骰子的平均值绘图

### 一元离散随机变量，可数论域

设随机变量$$ X $$获得值$$ x_1, x_2, \dots $$的概率分别是$$ p_1, p_2, \dots $$，则该随机变量的期望值是无限和
$$
\operatorname{E}[X]=\sum_{i=1}^{\infty}x_ip_i
$$
前提是此无限和[绝对收敛](https://en.wikipedia.org/wiki/Absolute_convergence)，否则称$$ X $$的期望值不存在。

### 一元不可数随机变量

如果$$ X $$的[概率分布](https://en.wikipedia.org/wiki/Probability_distribution)由一个概率密度函数$$ f(x) $$确定，则其期望值可被计算为
$$
\operatorname{E}[X]=\int_{-\infty}^{\infty}xf(x)\mathrm{d}x
$$
一般来说，如果$$ X $$的定义在[概率空间](https://en.wikipedia.org/wiki/Probability_space)$$ (\Omega, \Sigma, P) $$的随机变量，则$$ X $$的期望值，记为$$ \operatorname{E}[X] $$, $$ <x> $$, $$ \bar{x} $$, $$ \mathbf{E}[X] $$，定义为[勒贝格积分](https://en.wikipedia.org/wiki/Lebesgue_integration)
$$
\operatorname{E}[X]=\int_{\Omega}X\mathrm{d}P=\int_{\Omega}X(\omega)P(\mathrm{d}\omega)
$$
考虑到$$ X $$的概率密度函数$$ f(X) $$，$$ X $$的可测函数$$ g(X) $$的期望值由$$ f $$和$$ g $$的[內积](https://en.wikipedia.org/wiki/Inner_product)得到：
$$
\operatorname{E}[g(X)]=\int_{-\infty}^{\infty}g(x)f(x)\mathrm{d}x
$$
作为特殊情况，设$$ \alpha $$为正实数，有
$$
\operatorname{E}[|X|^\alpha]=\alpha\int_{0}^{\infty}t^{\alpha-1}P(|X|>t)\mathrm{d}t
$$
特别地，若$$ \alpha=1 $$且$$ P_r[X \geq 0]=1 $$，则简化为
$$
\operatorname{E}[|X|]=\operatorname{E}[X]=\int_{0}^{\infty}\{1-F(t)\}\mathrm{d}t
$$
这里$$ F $$是$$ X $$的累积分布函数。

## 性质

### 常量

$$
\operatorname{E}[c]=c
$$

### 单调

如果$$ X $$和$$ Y $$都是随机变量且几乎必然有$$ X \leq Y $$，则有$$ \operatorname{E}[X] \leq \operatorname{E}[Y] $$   

### 线性

$$
\operatorname{E}[X+c]=\operatorname{E}[X]+c
$$
$$
\operatorname{E}[X+Y]=\operatorname{E}[X]+\operatorname{E}[Y]
$$
$$
\operatorname{E}[aX]=a\operatorname{E}[X]
$$
上述公式即使在$$ X $$和$$ Y $$不独立的情况下也成立。结合起来就是
$$
\operatorname{E}[aX+bY+c]=a\operatorname{E}[X]+b\operatorname{E}[Y]+c
$$
对于两个离散随机变量$$X, Y$$，可定义如下[条件期望](https://en.wikipedia.org/wiki/Conditional_expectation)：
$$
\operatorname{E}[X|Y=y]=\sum_{x}x \cdot P(X=x|Y=y)
$$
说明$$ \operatorname{E}[X|Y=y] $$是$$ y $$的函数，其也单独表示了一个随机变量。   
定理：
$$
\operatorname{E}[X]=\operatorname{E}[\operatorname{E}[X|Y]]
$$
上式对连续随机变量也成立。

### 不等式

$$
|\operatorname{E}[X]| \leq \operatorname{E}[|X|]
$$

## 应用

经典力学中的重心是和期望值类似的概念。   
期望值也能用于计算方差：
$$
\operatorname{Var}(X)=\operatorname{E}[X^2]-(\operatorname{E}[X])^2
$$

参考资料：[维基百科](https://en.wikipedia.org/wiki/Expected_value)

# 方差

方差是一个随机变量到其均值的偏差的平方的期望。从非正式的角度其度量了一个（随机数）集合到他们均值的散布情况。方差是统计学中的核心概念。方差是标准偏差的平方，一般记为$$ \sigma^2 $$， $$ s^2 $$，或者$$ \operatorname{Var}(X) $$。   

## 定义

随机变量$$ X $$的方差是到$$ X $$的均值的偏差的平方的期望值：
$$
\operatorname{Var} = \operatorname{E}[(X-\mu)^2]
$$
这里$$ \mu = \operatorname{E}(X) $$。
同样可以用协方差的方式表示：
$$
\operatorname{Var}(X) = \operatorname{Cov}(X, X)
$$
方差的公式也能展开：
$$
\begin{align}
\operatorname{Var}(X)
&= \operatorname{E}[(X-\operatorname{E}[X])^2] \\
&= \operatorname{E}[X^2-2X\operatorname{E}(X)+(\operatorname{E[X]})^2] \\
&= \operatorname{E}[X^2] - 2\operatorname{E}[X]\operatorname{E}[X]+(\operatorname{E}[X])^2 \\
&= \operatorname{E}[X^2] - (\operatorname{E}[X])^2
\end{align}
$$

### 连续随机变量

如果随机变量$$ X $$表示从一个以$$ f(x) $$为概率密度函数的连续分布生成的取样，则其种群方差为
$$
\begin{align}
\operatorname{Var}(X) &= \sigma^2 \\
&= \int(x-\mu)^2f(x)dx \\
&=\int x^2f(x)dx-2\mu \int xf(x)dx+\int\mu^2f(x)dx \\
&=\int x^2f(x)dx - \mu^2
\end{align}
$$
因为$$ \int f(x)dx = 1 $$。
这里$$ \mu $$是期望值
$$
\mu=\int xf(x)dx
$$
没有期望值的分布也没有方差。

### 离散随机变量

如果生成随机变量$$ X $$的是离散概率质量函数$$ x_1 \mapsto p_1, x_2 \mapsto p_2, \cdots, x_n \mapsto p_n $$则
$$
\operatorname{Var}(X)  = \sum_{i=1}^{n}p_i \cdot (x_i-\mu)^2
$$
或等价地
$$
\operatorname{Var}(X)=\sum_{i=1}^{n}p_ix_i^2-\mu^2
$$
这里$$ \mu $$是期望值，即
$$
\mu = \sum_{i=1}^{n}p_i \cdot x_i
$$
$$ n $$个等概率的值的集合的方差可以写为
$$
\operatorname{Var}(X)=\frac{1}{n}\sum_{i=1}^{n}(x_i-\mu)^2
$$
$$ \mu $$是期望值
$$
\mu = \frac{1}{n}\sum_{i=1}^{n}x_i
$$
展开形式
$$
\begin{align}
\operatorname{Var}(X) &= \frac{1}{n^2}\sum_{i=1}^{n}\sum_{j=1}^{n}\frac{1}{2}(x_i-x_j)^2 \\
&= \frac{1}{n^2}\sum_i\sum_{j>i}(x_i-x_j)^2
\end{align}
$$

参考资料：[维基百科](https://en.wikipedia.org/wiki/Variance)

# 协方差

$$
\operatorname{cov}(X,Y)=\operatorname{E}\left[\left(X-\operatorname{E}\left[X\right]\right)\left(Y-\operatorname{E}\left[Y\right]\right)\right]
$$
$$
\begin{align}
\operatorname{cov}\left(X,Y\right)&=\operatorname{E}\left[\left(X-\operatorname{E}\left[X\right]\right)\left(Y-\operatorname{E}\left[Y\right]\right)\right] \\
&=\operatorname{E}\left[XY-X\operatorname{E}\left[Y\right]-\operatorname{E}\left[X\right]Y+\operatorname{E}\left[X\right]\operatorname{E}\left[Y\right]\right] \\
&=\operatorname{E}\left[XY\right]-\operatorname{E}\left[X\right]\operatorname{E}\left[Y\right]-\operatorname{E}\left[X\right]\operatorname{E}\left[Y\right]+\operatorname{E}\left[X\right]\operatorname{E}\left[Y\right] \\
&=\operatorname{E}\left[XY\right] - \operatorname{E}\left[X\right]\operatorname{E}\left[Y\right]
\end{align}
$$

参考资料：[维基百科](https://en.wikipedia.org/wiki/Covariance)

# 估计函数

一个估计函数或者点估计是一个统计量（即，数据的函数），用于推断在一个统计模型中未知参数的值。被估计的参数有时被称为被估量（estimand）。如果被估参数用$$ \theta $$表示则习惯上将其估计函数记为$$ \hat{\theta} $$。作为数据的函数，估计函数本身是一个随机变量，对其的特定实现称为“估计”。

## 定义

设有一个固定参数$$ \theta $$需要被估计。则一个“估计函数”是一个将样本空间映射到样本估计集合的函数。$$ \theta $$的一个估计函数通常记为$$ \hat{\theta} $$。

## 性质

### 误差

$$
e(x)=\hat{\theta}(x)-\theta
$$

### 平均平方误差

$$
\operatorname{MSE}(\hat{\theta})=
\operatorname{E}\left[\left(\hat{\theta}(X)-\theta\right)^2\right]
$$

### 取样偏差

$$
d(x)=\hat{\theta}(x)-\operatorname{E}\left(\hat{\theta}(X)\right)=\hat{\theta}(x)-\operatorname{E}(\hat{\theta})
$$

### 方差

$$
\operatorname{var}(\hat{\theta})=
\operatorname{E}\left[\left(\hat{\theta}-\operatorname{E}(\hat{\theta})\right)^2\right]
$$

### 偏差

$$
B(\hat{\theta})=\operatorname{E}(\hat{\theta})-\theta
$$

### 联系

$$
\operatorname{MSE}(\hat{\theta})=\operatorname{var}(\hat{\theta})+\left(B(\hat{\theta})\right)^2
$$

参考资料：[维基百科](https://en.wikipedia.org/wiki/Estimator)

# 回归分析

在统计建模中，回归分析是估算变量间的关系的统计过程。当焦点是一个因变量和一个或多个自变量之间的联系时，其包含了许多方法用来对多个变量分析和建模。更具体地，回归分析帮助人们弄清当任一自变量变化而其他自变量不变时，因变量是如何变化的。最常见地，回归分析估算在给定自变量的情况下因变量的[条件期望](https://en.wikipedia.org/wiki/Conditional_expectation)，即当自变量固定某个值时，因变量的平均值。较少见的焦点是同样情况下条件期望的分位点或者其他位置参数。在所有情况下，估算的目标是自变量的一个函数，称为回归函数。在回归分析中，另一个兴趣点是针对能被描述为一个概率分布的回归函数，因变量围绕其变化的特性。如果针对给定的自变量值，求因变量的最大值而不是平均值。   
回归分析被广泛用于预报和预测，其应用于机器学习领域有很多重合。回归分析也用来弄清多个自变量中哪个与因变量相关，以及这种关系的形式。   
已经开发出的进行回归分析的方法有很多。较熟悉的如果线性回归和普通最小二乘法回归是参数的，因为回归函数用从数据估算出的有限个未知参数定义。非参数回归指的是允许回归函数位于特定的函数集合中的方法，这些函数可以是无穷维度的。   
在实践中回归分析方法的性能依赖于[数据生成过程](https://en.wikipedia.org/wiki/Data_collection)的形式，以及其是如何与被利用的回归方法相联系的。   
狭义来说，回归可特指对连续反应变量的估算，与之相反的是用于分类的离散反应变量。

## 回归模型

回归模型涉及以下变量：

+ 未知参数，记为$$ \beta $$，可表示一个标量或向量。
+ 自变量， $$ X $$。
+ 因变量， $$ Y $$。

一个回归模型将$$ Y $$联系到$$ X $$和$$ \beta $$的函数：
$$
Y \approx f(X,\beta)
$$
该近似通常被正规化为$$ \operatorname{E}(Y|\pmb{X})=f(\pmb{X},\pmb{\beta}) $$。为实现回归分析，必须指定函数$$ f $$的形式。   
设未知向量参数$$ \beta $$长度是$$ k $$。为进行回归分析用户必须提供的关于因变量$$ Y $$的信息，设观察到的点的形式是$$ (Y,\pmb{X}) $$，数量是$$ N $$。则$$ N<k $$时无法进行回归分析；$$ N=k $$时且函数$$ f $$是线性的，则上述回归模型能精确求解（应该就是用线性方程组求得唯一解），只要$$ X $$是线性无关的。如果函数$$ f $$是非线性的，则可能无解或者许多解。如果$$ N>k $$是最常见的情况，可有足够的信息来估算$$ \beta $$的唯一值。

## 基本假设

对回归分析的经典假设包含：

+ 取样对推断预测的种群具有代表性。
+ 误差是一个均值为0的随机变量（conditional on the explanatory variables？）。
+ 自变量的测量没有误差。
+ 自变量是线性无关的，即任何一个预测器（predictor）都无法用其他预测器的线性组合来表示。但并不是无法表示。自变量、自变量的平方、自变量的立方的组合没问题。
+ 误差是不相关的。（[方差-协方差矩阵](https://en.wikipedia.org/wiki/Covariance_matrix)？）
+ 误差的方差在多次观察时保持[恒定](https://en.wikipedia.org/wiki/Homoscedasticity)。否则，应该使用[加权最小二乘法](https://en.wikipedia.org/wiki/Weighted_least_squares)或者其他方法。

这些假设足够使用最小二乘法估计函数来处理期望性质；特别地，这些假设意味着参数的估计在线性无偏差估计函数中将是无偏差的，一致的和有效的。

参考资料：[维基百科](https://en.wikipedia.org/wiki/Regression_analysis)

# 趋均数回归（regression to the mean）

趋均数回归代表了一种现象，即当一个变量在其第一次被测量时呈现极值，则其第二次测量会离平均值更近，且如果在第二次测量出现极值，则其第一次测量会离平均值更近。为避免进行错误推断，在设计科学实验和解释数据时必须考虑趋均数回归。   
趋均数回归可用任意具有相同边缘分布的二元分布定义。   
趋均数回归并不是一个因果现象，所以并不是必定出现在某个个体身上，还有其他因素也要考虑。
参考资料：[维基百科](https://en.wikipedia.org/wiki/Regression_toward_the_mean)

# 高斯-马尔科夫定理

陈述一个线性回归模型中，若误差满足期望值为0、且互不相关、拥有相等的方差，则其系数的最优线性无偏差估计函数（BLUE：best linear unbiased estimator)被[普通最小二乘法](https://en.wikipedia.org/wiki/Ordinary_least_squares)估计函数给定。这里“最优”指的是估算的方差最低，通其他无偏差的线性估计函数比较。误差不需要正态分布，也不需要[独立同分布](https://en.wikipedia.org/wiki/Independent_and_identically_distributed)。   

# 陈述

设我们将简化的矩阵记法
$$
\underline{y}=X\underline{\beta}+\underline{\varepsilon}, \quad
(\underline{y},\underline{\varepsilon}\in\mathbb{R}^n,\underline{\beta}\in\mathbb{R}^K\text{and}X\in\mathbb{R}^{n\times K})
$$
展开为
$$
y_i=\sum_{j=1}^{K}\beta_jX_{ij}+\varepsilon_i\quad \forall i=1,2,\cdots,n
$$
这里$$ \beta_j $$是非随机但不可观察的参数，$$ X_{ij} $$是非随机且可观察的（称为解释变量 explanatory variables），$$ \varepsilon_i $$是随机的，因此$$ y_i $$是随机的。随机变量$$ \varepsilon_i $$称为干扰、噪音或误差（与[残差](https://en.wikipedia.org/wiki/Errors_and_residuals_in_statistics)相对）。如果需要多加常量，将最后几个$$ X $$的值设为1即可。   
高斯-马尔科夫的假设关注误差随机变量$$ \varepsilon_i $$的集合：

+ 他们的均值为0： $$ \mathbb{E}[\varepsilon_i]=0 $$
+ 他们[同方差](https://en.wikipedia.org/wiki/Homoscedasticity)，即都有相同的有限方差：$$ \operatorname{Var}(\varepsilon_i)=\sigma^2<\infty $$
+ 不同的误差互不相关： $$ \operatorname{Cov}(\varepsilon_i,\varepsilon_j)=0,\forall i\neq j $$

一个$$ \beta_j $$的线性估计函数是一个线性组合
$$
\hat{\beta}_j=c_{1j}y_1+\cdots+c_{nj}y_n
$$
这里系数$$ c_{ij} $$不允许依赖于$$ \beta_j $$，因为它是无法观察的。但是其可以依赖$$ X_{ij} $$的值，因为这些数据可被观察。称估计函数是无偏差的，当且仅当不论$$ X_{ij} $$的值，有
$$
\mathbb{E}\left[\hat{\beta}_j\right]=\beta_j
$$
现在设$$ \textstyle\sum_{j=1}^{K}\lambda_j\beta_j $$为系数的某些线性组合。则对应估计函数的[均方误差](https://en.wikipedia.org/wiki/Mean_squared_error)为
$$
\operatorname{E}\left[\left(\sum_{j=1}^K\lambda_j\left(\hat{\beta}_j-\beta_j\right)\right)^2\right]
$$
参数$$ \beta_j $$的向量$$ \beta $$的最优线性无偏差估计函数是对于线性组合参数的每个向量$$ \lambda $$都有最小的均方误差。这等价于
$$
\operatorname{Var}(\tilde{\beta})-\operatorname{Var}(\hat{\beta})
$$
对于每个其他线性无偏差估计函数$$ \tilde{\beta} $$是正半定矩阵。   
普通最小二乘法估计式是函数
$$
\hat{\beta}=(X'X)^{-1}X'y
$$
$$ y $$和$$ X $$将最小化残差平方和：
$$
\sum_{i=1}^{n}(y_i-\hat{y}_i)^2=
\sum_{i=1}^{n}\left(y_i-\sum_{j=1}^K\hat{\beta}_jX_{ij}\right)^2
$$
定理表明普通最小二乘法估计式记为一个最优线性无偏差估计函数。
参考资料：[维基百科](https://en.wikipedia.org/wiki/Gauss%E2%80%93Markov_theorem)

# 残差（residual）-数值计算

粗略来讲，残差是结果的误差。确切地说，设我们要寻找$$ x $$使其满足
$$
f(x)=b
$$
给定$$ x $$的一个近似值$$ x_0 $$，残差就是
$$
b-f(x_0)
$$
而误差则是
$$
x-x_0
$$
如果我们不能准确地知道$$ x $$，我们就没法计算误差，但是我们能够计算残差。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/Residual_(numerical_analysis))

# 误差与残差-统计学和最优化

误差（扰动）是一个被观察对象的观测值和其真实值之间的偏离量（如总体平均值），而被观察对象的残差是观测值与估计值之间的差异（如样本平均值）。两者的差异对回归分析最为重要。   
统计学误差是观测值与其期望值的差异，后者基于随机选择单位的整个种群。期望值，即整个种群的均值，一般是无法观察的，也因此统计学误差也不能被观察。   
而另一方面，残差（或拟合偏差）是一个不可观察的统计学误差的一个可观察的估计。   
一个随机采样中的残差的和必须为0，因此残差也必须不是独立的。而统计学误差是独立的，在随机样本中它们的和几乎必然不为0。   
设一个种群呈正态分布，均值为$$ \mu $$，标准偏差为$$ \sigma $$，独立地选择个体，则有
$$
X_1,\cdots,X_n\sim N(\mu,\sigma^2)
$$
取样均值
$$
\overline{X}=\frac{X_1+\cdots+X_n}{n}
$$
是随机变量，则有
$$
\overline{X}\sim N(\mu,\sigma^2/n)
$$
统计学误差即为
$$
e_i=X_i-\mu
$$
而残差为
$$
r_i=X_i-\overline{X}
$$
统计学误差的平方和，再除以$$ \sigma^2 $$，有$$ n $$自由度的卡方分布：
$$
\frac{1}{\sigma^2}\sum_{i=1}^{n}e_i^2\sim\chi_n^2
$$
然而，该数量在种群密度未知时是无法观察的。另一方面，残差的平方和却可观察：
$$
\frac{1}{\sigma^2}\sum_{i=1}^{n}r_i^2\sim\chi_{n-1}^2
$$
一定要对残差进行绘图检查！（如何做？）
参考资料：[维基百科](https://en.wikipedia.org/wiki/Errors_and_residuals)

# p-值

p-值代表了一个概率，即使用给定的统计模型，获得的统计概要与实际观察结果相同或者更为极端的概率。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/P-value)

# 优势率

优势率是量化在一个种群中，存在或不存在属性A和存在与不存在属性B之间联系的强度。如果种群中每个个体都有或没有属性A，同样也有或没有属性B，且两种属性都被恰当地定义，则能够得出一个比率，用于量化描述种群个体存不存在属性A与存不存在属性B的联系。计算步骤如下：

1. 对给定存在B的个体计算其有A的几率
2. 对给定不存在B的个体计算有A的几率
3. 用1中的结果除以2中的结果即为所求

如果优势率大于1，则存在A可被视为与存在B相联系，即存在B（相对于不存在B）提升了存在A的几率。注意这不表明B的A的成因之一，这种联系可能是因为第三属性，C，同时是A和B的成因之一（[混淆](https://en.wikipedia.org/wiki/Confounding)）。   
其他两种量化联系的主要方法是[危险比](https://en.wikipedia.org/wiki/Risk_ratio)和[绝对危险降低率](https://en.wikipedia.org/wiki/Absolute_risk_reduction)。

## 定义

优势率是一个组中事件发生的几率和另外的组中发生几率的比值。如果在两个组中事件发生的概率分别是$$ p_1 $$和$$ p_2 $$，则优势率为
$$
\frac{p_1/(1-p_1)}{p_2/(1-p_2)}=\frac{p_1/q_1}{p_2}{q_2}=\frac{p_1q_2}{p_2q_1}
$$
这里$$ q_x=1-p_x $$。优势率为1表示被研究的事件在两个组中有相同发生的可能，大于1表示事件在第一组中更可能发生，小于1则在第一组中更不可能发生。优势率只在非负时有意义。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/Odds_ratio)

# 几率

在统计学中，事件E的几率是其发生的概率的一个简单函数。解释几率的自然方法是长远来看，发生该事件和发生其他事件的比率。比如一个公平的骰子，roll到6的几率是1比5。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/Odds)

# 混淆变量

混淆变量是统计模型的额外变量，且同时和自变量、因变量（直接或反向地）相关，解释了这些变量间相关的部分或全部原因。    
本质上一个混淆变量遵循以下四个标准，这里感兴趣的变量为V，混淆变量为C，感兴趣的变量输出为O：

1. C与O（间接或反向地）关联
2. C与O关联，独立于V
3. C与V（间接或反向地）关联
4. C并不在V到O的因果路径上（C不是V的直接结果，也不在V产生O的路径上）

参考资料：[维基百科](https://en.wikipedia.org/wiki/Confounding)

# 相关（correlation）

相关是统计学中涉及到依赖的广泛的关系类别的统称，尽管常用于指两个变量间有着线性关系。

## [皮尔逊积差系数](https://en.wikipedia.org/wiki/Pearson_product-moment_correlation_coefficient)

获得方法：两个变量的协方差除以它们标准偏差的积。设两个随机变量$$ X $$和$$ Y $$，它们的期望值分别为$$ \mu_X $$和$$ \mu_Y $$、标准偏差分别是$$ \sigma_X $$和$$ \sigma_Y $$，则它们的种群相关系数$$ \rho_{X,Y} $$为
$$
\rho_{X,Y} = \operatorname{corr}(X,Y) = \frac{\operatorname{cov}(X,Y)}{\sigma_X\sigma_Y} = \frac{\operatorname{E}\left[(X-\mu_X)(Y-\mu_Y)\right]}{\sigma_X\sigma_Y}
$$
参考资料：[维基百科](https://en.wikipedia.org/wiki/Correlation_and_dependence)

# 逻辑回归

逻辑回归是一个统计模型，其因变量是分类的。以下描述的二分因变量，即其仅能有两个值，如顺利/失败、活着/死亡。情况多于两个的，有[多项逻辑回归](https://en.wikipedia.org/wiki/Multinomial_logistic_regression)，又或者多个分类是有序的，如[顺序逻辑回归](https://en.wikipedia.org/wiki/Ordinal_logistic_regression)。  
逻辑回归用于测量分类因变量同一个或多个自变量之间的联系，方法是使用一个具有累积逻辑分布的[逻辑函数](https://en.wikipedia.org/wiki/Logistic_function)来估计概率。逻辑回归可看作是[一般化的线性模型](https://en.wikipedia.org/wiki/Generalized_linear_model)的特例，因此和线性回归类似。但两者也有很大区别。首先，条件分布$$ y | x $$是伯努利分布而不是高斯分布，因为因变量是二态的。其次，自变量的值的概率也通过[逻辑分布函数](https://en.wikipedia.org/wiki/Logistic_function)限制到(0,1)因为逻辑回归预测的是特定输出的概率。

## 潜变量解释

逻辑回归能简单地解释为查找参数$$ \beta $$使之适合：
$$
y =
\begin{cases}
1 &\quad \beta_0+\beta_1x+\varepsilon>0 \\ 0 &\quad \text{else}
\end{cases}
$$
这里$$ \varepsilon $$是误差，其分布为标准逻辑分布。   
相关联的潜变量是$$ y'=\beta_0+\beta_1x+\varepsilon $$。误差$$ \varepsilon $$无法观察，因此$$ y' $$也无法被观察，因此是“潜在的”。然而，参数$$ \beta $$不能直接用观测值 $$ y $$ 和 $$ x $$ 的公式表示，而是通过一个迭代搜索过程被发现，通常由软件程序完成。   
逻辑函数有用之处在于它能以所有实数$$ t, (t \in \mathbb{R}) $$为输入，而输出值则永远在0到1之间，因此可被解释为概率。逻辑函数$$ \sigma(t) $$定义如下：
$$
\sigma(t)=\frac{e^t}{e^t+1}=\frac{1}{1+e^{-t}}
$$
我们可假设$$ t $$是单个解释变量$$ x $$的线性函数（$$ t $$是多个解释变量的线性组合的情况可用类似方法处理）。我们可将$$ t $$如下表示：
$$
t=\beta_0+\beta_1x
$$
而逻辑函数则可写为：
$$
F(x)=\frac{1}{1+e^{-(\beta_0+\beta_1x)}}
$$
$$ F(x) $$解释为因变量为真或成功的概率。注意响应变量$$ Y_i $$并不是同分布的：$$ P(Y_i=1|X) $$随着每个不同的点$$ X_i $$而不同，尽管它们的参数$$ \beta $$是一样的。   
逻辑函数的[反函数](https://en.wikipedia.org/wiki/Logit)$$ g $$定义如下：
$$
g(F(x))=\ln \left(\frac{F(x)}{1-F(x)}\right) = \beta_0+\beta_1x
$$
等价地，两边同时求指数幂：
$$
\frac{F(x)}{1-F(x)}=e^{\beta_0+\beta_1x}
$$
因为$$ F(x) $$代表的是概率，所以从上式可得因变量等于某个情况的几率，就是以线性回归表达式为指数的幂。对于一个连续自变量，优势率可定义如下：
$$
\mathrm{OR} = \frac{\operatorname{odds}(x+1)}{\operatorname{odds}(x)} = \frac{\left(\frac{F(x+1)}{1-F(x+1)}\right)}{\left(\frac{F(x)}{1-F(x)}\right)} = \frac{e^{\beta_0+\beta_1(x+1)}}{e^{\beta_0+\beta_1x}} = e^{\beta_1}
$$
因为该模型可以用[广义线性模型](https://en.wikipedia.org/wiki/Generalized_linear_model)表示，对于 $$ 0<p<1 $$，[普通最小二乘法](https://en.wikipedia.org/wiki/Ordinary_least_squares)已经足够；当 $$ p=0\,\text{or}\,1 $$ 时，需要用到更复杂的方法。  
参考资料：[维基百科](https://en.wikipedia.org/wiki/Logistic_regression)

# 似然函数

似然函数是统计模型的参数的函数，模型已经有给定数据。似然函数在[统计推断](https://en.wikipedia.org/wiki/Statistical_inference)中扮演关键角色，尤其是对从一组统计数据中估计参数的方法而言。在非正式场合，“似然”经常用作概率的同义词，而在统计学中，区别它们的是角色定位于输出还是参数。概率用在数据获取之前，用于描述将来获得给定输出值的概率，在有参数的前提下。似然用在数据获取之后，用于描述参数（或参数向量）的一个函数，针对给定的输出。   

## 定义

给定输出$$ x $$，一组参数值的似然，$$ \theta $$，等于那些观察值，在给定这些参数值时出现的概率，即
$$
\mathcal{L}(\theta|x) = P(x|\theta)
$$

### 离散概率分布

设$$ X $$是一个随机变量，有离散概率分布$$ p $$，且其分布依赖于参数$$ \theta $$。则函数
$$
\mathcal{L}(\theta|x) = p_\theta(x) = P_\theta(X=x)
$$
还可记作$$ P(X=x|\theta) $$、$$ P(X=x;\theta) $$。

### 连续概率分布

设$$ X $$是一个随机变量，遵循绝对连续概率分布，其密度函数$$ f $$依赖参数$$ \theta $$。则
$$
\mathcal{L}(\theta|x) = f_\theta(x)
$$

### 对数似然函数

对于许多应用，似然函数的自然对数，称为对数似然函数，能更为方便地运用。因为对数是单调递增函数，函数的对数在函数获得最大值的点同时获得最大值，因此对数似然函数能够在最大似然估计和相关的方法中代替似然函数。查找函数的最大值经常需要对函数求导并对最大化的参数求解，此时如果最大化的是对数似然函数就更简单。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/Likelihood_function)

# 最大似然估计

最大似然估计（MLE: maximum likelihood estimation）是估计统计模型的参数的方法，在给定观测值后，通过查找使得观测值和参数构成的似然函数获得最大值的参数值。

## [原理](https://en.wikipedia.org/wiki/Likelihood_principle)

设有$$ n $$次独立、同分布的观察组成的取样$$ x_1,x_2,\cdots,x_n $$，来自某个未知概率密度函数$$ f_0(\cdot) $$的分布。然而能够推测函数$$ f_0 $$属于一个特定的分布家族 $$ \{f(\cdot\mid\theta),\theta\in\Theta\} $$ (这里 $$ \theta $$ 是家族中的一个参数向量)，称为参数模型，于是有$$ f_0=f(\cdot\mid\theta_0) $$。$$ \theta_0 $$ 代表着参数向量的真实值，且是未知的。理想的情况是找到一个估计值 $$ \hat{\theta} $$，能够尽可能的靠近真实值 $$ \theta_0 $$。   
为使用最大似然估计方法，首先需要为所有观察指定[联合密度函数](https://en.wikipedia.org/wiki/Probability_density_function#Densities_associated_with_multiple_variables)。对一个独立、同分布的取样，联合密度函数为
$$
f(x_1,x_2,\cdots,x_n\mid\theta) = f(x_1\mid\theta) \times f(x_2\mid\theta) \times \cdots \times f(x_n\mid\theta)
$$
现在我们换个角度来看这个函数，将观测值 $$ x_1,x_2,\cdots,x_n $$ 视为该函数固定的“参数”，而 $$ \theta $$ 为函数的变量允许其自由变化；这个函数就称为似然函数：
$$
\mathcal{L}(\theta\,;x_1,x_2,\cdots,x_n) =
f(x_1,x_2,\cdots,x_n\mid\theta) =
\prod_{i=1}^{n}f(x_i\mid\theta)
$$
在实践中更经常地使用似然函数的对数形式更简便，即对数似然函数：
$$
\ln\mathcal{L}(\theta\,;x_1,\cdots,x_n) =
\sum_{i=1}^{n}\ln f(x_i\mid\theta)
$$
或平均对数似然函数：
$$
\hat{\ell} = \frac{1}{n}\ln\mathcal{L}
$$
最大似然估计方法发现 $$ \theta $$ 的值使得 $$ \hat\ell(\theta\,;x) $$ 最大化，以此估计 $$ \theta_0 $$ 的值。这就定义了 $$ \theta_0 $$ 的最大似然估计：
$$
\{\hat\theta_\mathrm{mle}\} \subseteq
\{\underset{\theta\in\Theta}{\operatorname{arg\,max}}\:\hat\ell(\theta\,;x_1,\cdots,x_n)\}
$$
如果最大值存在。对许多模型而言，作为观察数据 $$ x_1,x_2,\cdots,x_n $$ 的显示函数，最大似然估计能被找到。然而如果已知或有用的最大化问题没有闭合式的解决方案，最大似然估计只能通过数值优化方法发现。   
参考资料：[维基百科](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation)

# 置信区间

置信区间是[种群参数](https://en.wikipedia.org/wiki/Statistical_parameter)的区间估计的一种，一种通过观测值计算得到区间，大体上不同的取样其值不同，其中有可能包含了无法被观测的真实目标参数。如果实验不断重复，观测到的包含了真实参数的区间的频率称为 *置信级* 。换句话说，如果置信区间的建立方法是对相同种群进行分离的实验，每次实验的过程相同，则这样的区间包含了参数真实值的比例将和置信级相同。而置信区间的边界称为低/高置信界限。

参考资料：[维基百科](https://en.wikipedia.org/wiki/Confidence_interval)
