---
---

# 退出命令

```
> q()
```
# 帮助

```
> help(str)
> ?str
```
会打开帮助文档网页   
`help.search`，另外的方式是`??str`   

+ 执行脚本文件：`> source("*.R")`， Windows 环境下菜单里有。`> sink("result.lis")` 将所有接下来的输出转移到外部文件， `> sink()` 则会将之前的信息重新在控制台显示。
+ R 创建和操作的实体称为对象。 `> objects()` 可显示当前 R 中存储的对象。当前存储对象的集合称为工作空间。
+ `rm` 函数用来移除对象。一次 R 会话中创建的所有对象都可以永久地存储到文件中，并在将来的 R 会话中使用。退出时信息保存在 `.RData` 和 `.Rhistory` 中。

# 简单操作

+ `c()` 函数用于创建向量，而 `<-` 用于赋值，大部分情况可用 `=` 代替，另有函数 `assign` 用两个参数的形式完成赋值。赋值也可以反方向完成，用 `->`。
+ `c()` 函数中有参数是向量的，展开然后合并。
+ 向量的算术都是一个元素一个元素进行的。参与运算的向量不一定要等长，而结果向量长度为最长参数向量的长度，其余的向量通过循环补齐不足的元素。
+ `+,-,*,/,^`，最后一个是乘方。`log, exp, sin, cos, tan, sqrt, max, min, range, length, sum, prod, mean, var, sort`
+ 生成序列，`:` 和 Python 中的 slice 意义一样，且其可以与其他运算结合，而优先级高于四则运算，比乘方优先级低。
+ `seq()` 函数类似于 Python 中的 `linspace`。但可以不用每次指定起始和结束，也可以 `from` 和 `by` 加上 `length`。
+ `rep()` 函数，复制参数向量。 `times` 参数指定向量被重复几次， `each` 则指定每个元素重复几次然后再继续下一个。
+ 逻辑运算： `<, <=, >, >=, ==, !=, &, |, !`
+ 缺失值为 NA。函数 `is.na()` 可判断向量中有否 NA，给出类似 Python 中的 mask 数组。另一个缺失值为 NaN。`is.na()` 对两者都是真，而 `is.nan()` 则只对 NaN 为真。
+ `paste()` 函数可有任意数量的参数，然后用向量的方式对每组一个元素接一个元素地连接起来，循环过程类似 Python 中的 `zip`。 `sep` 参数指定连接符号，默认为空格。
+ 索引元素仍然用中括号，其中的参数可以是向量。可在中括号中进行逻辑判断，为真的就被选中；还可以是正整数向量，可以是计算得到正整数向量的表达式；如果是负整数向量，则是排除那些元素；如果对象有 `names` 属性，比如用 `names()` 函数赋值过，则也可以用字符串当参数。
+ 除了过滤出需要的元素，也可以对这些元素赋值，比如将 `is.na` 为真的元素赋 0 值。
+ 除了向量，还有其他对象：矩阵，即多维数组，实际上也是元素为向量的向量； factor 提供了处理分类数据的简便方法；list 类似向量，但是不需要元素的类型相同，且也可以嵌套 vector 和 list，对返回计算结果很有帮助；data frame 应该和 Python 中的类似；最后是 function。

# 对象及其模式和属性

+ 向量的值必须都是相同的模式，逻辑、数组、负数、字符串或 raw。模式 `mode` 即对象的元素的基础类型，是对象的属性的特例。其它属性有 `length`。这两者是对象的内置属性。提供属性的方式是 `attributes(object)`。
+ 使用 `as.something()` 可以更改向量的模式。`numeric()` 和 `character()` 分别创建空的数值和字符串向量。可以在初始化向量时使用参数索引，然后只赋一个值，则向量变成相应长度，且之前的值均为 Na。通过运算赋值即可改变向量的元素和长度，或者对 `length()` 赋值。
+ `attributes(object)` 返回对象当前定义的所有非内置属性的列表。`attr(obj, name)` 可以选择一个特定属性。此函数被赋值则可以改变、创建指定的属性。
+ R 中每个对象都有其类，简单向量的类即它们的模式。

# 有序和无序 factor

+ factor 是一个向量对象，用来指定相同长度的其他向量的元素的离散分类。`factor(obj)` 和 `levels(factor_obj)`。后者应该是去重复。`tapply()` 以向量、其 factor、操作为参数，比如对所有 level 求平均。
+ 求 95% 的置信区间：`2 * qt(0.975, n - 1) * stderr / sqrt(n)`

# 数组和矩阵

+ 矩阵就是二维数组。数组有维度向量，元素全为非负整数，其长度即为数组的维度。
+ 一个向量只有在有一个维度向量作为其 `dim` 属性时才能被 R 视为数组。可以通过 `dim(obj) <- c(x,y,z)` 做到。
+ 元素在数组中的排列，还是从最靠近左边的维开始。对子集的选择：如果某个维没有给任何值，则相当于 Python 中的 slice 只给一个 `:`，等于是该维的全部元素。
+ 必须显式地使用 `dim(Z)` 来引用数组的维度向量。
+ 可用一个矩阵来作为索引，这样可以从矩阵中获得不规则的元素。不能用负数索引。
+ 外积或叉积或矢量积： `%o%`，同时还有函数 `outer()`，后者可以函数为参数。
+ `aperm()` 函数
+ `t()` 矩阵转置， `nrow(), ncol()`，矩阵乘法 `%*%`， `crossprod()` 叉乘，即 `t(X) %*% y == crossprod(X, y)` 但是后者更高效。
+ `diag()` 函数，参数是向量则让矩阵的对角称为参数，参数是矩阵则返回参数的对角元素。如果参数是正整数，则生成 k x k 单位矩阵。
+ `solve(A, b)` 对线性方程组求解。
+ 二次型 $$ x^TA^{-1}x $$ 求法：`x %*% solve(A, x)`。
+ `ev <- eigen(Sm)` 对对称矩阵求特征值和特征向量。`ev$val` 是特征值， `ev$vec` 是特征向量。
+ `svd()` 函数对任意矩阵参数进行奇异值分解。返回值是一个列表，有三个元素，`d, u, v` 分别代表结果矩阵和向量。
+ `lsfit()` 函数同样返回列表，里面是最小平方拟合过程的结果。一般有两个参数，`X` 为设计矩阵，`y` 为观测值向量。`ls.diag()` 函数用于回归诊断。回归建模用 `lm(.)` 函数。
+ `qr()` 函数进行 QR 分解。
+ `cbind()` 函数将矩阵、向量一列列地（即水平地）组合成新矩阵；`rbind()` 函数类似，却是一行行地（即垂直地）组合。
+ 如果要将一个数组变成一维向量，可用 `as.vector(X)` 函数。而达到同样目的的可以是不加更多参数的 `c(X)` 函数。
+ 一对 factor 可以定义双路交叉分类。 `table()` 函数可从等长的 factor 对中计算频率表、列联表。

# 列表和数据框架

+ R的列表是由有序的对象元素构成的。列表的下标运算符是 `[[]]`。同时列表名与字段名用 `$` 连接也可访问元素。如果字段名用在下标运算符中，要加双引号。可用字段名与下标运算符用分号组合，然后赋值给另外的变量。
+ 字段名不需要写完整，可以是简写，只要到足够辨识其元素的程度即可。
+ `list()` 可用来创建列表。参数可以是多个字段名和对象的组合。
+ 当 `c()` 函数的参数是列表时，返回的结果是列表对象。
+ 数据框架是一个列表，而其类是 data.frame。不是所有的列表都能变成数据框架，限制为：元素必为向量、factor、数值矩阵、列表或其他数据框架；矩阵、列表和数据框架提供的元素数量分别与它们的列、元素数量、变量数量相同；数值向量、逻辑向量和 factor 被原样包含进来，默认情况下字符串向量强制为 factor，其层则为向量中的唯一值集合；参数中的向量结构必须都有相同的长度，矩阵结构必须有相同的行大小。
+ 从很多目的来说，数据框架可以视为不同列可以有不同模式和属性的元素的矩阵。
+ `data.frame` 可以用来构造数据框架，参数是和列表构造类似，但要符合上述限制。符合限制的列表可用 `as.data.frame()` 来强制转换为数据框架。`read.table()` 可从文件中读取信息，创建数据框架。
+ `attach()` 将数据库附加到 R 搜索路径。这意味着可以不用限定名而直接访问数据库的字段。但是可以读取，更改不了。加了数据库限定名的才能使得更改永久生效。逆操作是 `detach()`。`attach` 的参数可以是列表。
+ `search()` 函数显示了当前搜索路径。

# 从文件读取数据

+ 为了能用 `read.table()` 函数读取数据，外部文件需要特殊的格式：第一行必须为每个变量的名称；其余行的第一个元素必为行标签，然后才是其它元素。参数 `head` 为真则可省略行标签。
+ `scan()` 函数
+ `edit(), fix()` 函数。

# 概率分布

针对不同分布，提供的函数包括计算累积分布函数，概率密度函数和 quantile function（给定 q，最小的 x 使得 $$ P(X \leq x) > q $$，以及模拟分布数据。   

| Distribution | R name | additional arguments |
|---|---|---|
| beta | beta | shape1, shape2, ncp |
| binomial | binom | size, prob |
| Cauchy | cauchy | location, scale |
| chi-squared | chisq | df, ncp |
| exponential | exp | rate |
| F | f | df1, df2, ncp |
| gamma | gamma | shape, scale |
| geometric | geom | prob |
| hypergeometric | hyper | m, n, k |
| log-normal | lnorm | meanlog, sdlog |
| logistic | logis | location, scale |
| negative binomial | nbinom | size, prob |
| normal | norm | mean, sd |
| Poisson | signrank | n |
| Student's t | t | df, ncp |
| uniform | unif | min, max |
| Weibull | Weibull | shape, scale |
| Wilcoxon | wilcox | m, n |

在 `name` 前加前缀 `d` 表示密度，`p` 表示 CDF， `q` 表示 quantile function，`r` 表示模拟。   

+ 测试数据集的分布：`summary, fivenum, stem`
+ `hist` 用于画柱状图，`density， ecdf， shapiro.test, ks.test, t.test, var.test, wilcox.test`

# 分组、循环和条件执行

+ 多个命令可以通过大括号连接成语句块。
+ `if (expr_1) expr_2 else expr_3`，`expr_1` 必须返回单个逻辑值。短路符号 `&&, ||`仅对长度为 1 的向量使用。`&, |` 是对向量的每个元素使用。
+ `ifelse(condition, a, b)` 类似 Python 中的 mask 数组，返回和 condition 长度相同的向量，为真的地方返回对应 a 中的值，为假的地方返回对应 b 中的值。
+ `for (name in expr_1) expr_2`，`repeat expr`， `while (condition) expr`。`break` 可用来打断循环，`next` 类似其他语言中的 `continue`。一般的表达式都是对整个向量或者数组操作，所以循环语句用得很少。更多的是用在函数中。
+ `split`

# 函数

+ 定义：`> name <- function(arg_1, arg_2, ...) expression`
+ `methods(class="data.frame")` 可用查看类可用的函数。

# R 中的统计模型

+ 基本的拟合普通多模型的函数是 `lm()`：`> fitted.model <- lm(formula, data = data.frame)`
+ 方差分析 `aov(formula, data = data.frame)`
+ `update()` 函数可以很方便地让一个模型根据之前拟合的结果，在添加或删除项目后再进行拟合：`> new.model <- update(old.model, new.formula)`

# 绘图进程

+ 以下函数会被自动调用：UNIX 上是 `X11()`、Windows 上是 `windows()`、MacOS 上是 `quartz()`。`dev.new()` 可以用来创建新的设备。
+ 绘图命令分为基本的三类：高层的、低层的、交互的。
+ 高层的最常用的是 `plot()` 函数。如果 X 是一个数值矩阵， `pairs(X)` 会将 X 的不同列两两绘制出来，都是 scatter 图。涉及到 3 到 4 个变量的图可以用 `coplot(|)` 绘制。用 `panel` 参数可以自定义上两个函数的图的类型。
+ `qqnorm(), qqline(), qqplot()`， `hist(), dotchart(), image(), contour(), persp()`
+ `add=TRUE, axes=FALSE, log="xy", type="p/l/b/o/h/s/S/n", xlab/ylab=str, main=titlestr, sub=x-axis-str,`
+ 低层的命令，`points(), lines()` 添加到当前图。`text()` 将文字添加到指定位置。`abline()` 添加指定斜率的直线到当前图。`polygon()` 根据给定的点绘制多边形。`legend(), title(), axis()`
+ `expression()` 可用于在图中添加数学符号。帮助：`help(plotmath), example(plotmath), demo(plotmath)`
+ `help(Hershey), demo(Hershey), help(Japanese), demo(Japanese)`
+ `locator()` 用于和鼠标左键交互。`identify()` 指出鼠标所指点的信息。
+ 图形参数，`par()` 可用于返回图形参数值，或者修改参数值。用此函数修改，是永久生效。如果在绘制图形的函数内用参数形式传递，则是临时修改。`pch, lty, lwd, col, col.{axis, lab, main, sub}, font, font.{axis, lab, main, sub}, adj, cex, cex.{...}`
+ 轴和刻度标记：`lab()` 刻度和刻度标签。`las` 轴标签朝向。 `mgp` 轴元素的位置。`tick` 刻度长度。`xaxs, yaxs` 两个轴的样式。
+ `mai, mar` 边缘留空。`mfcol, mfrow` 多个图构成的图集的大小。`mfg, fig` 当前图的位置。`oma, omi` 留空。

# 包

+ 查看已经安装了的包：`library()`。加入参数就是载入指定的包。
+ `install.packages(), update.packages()` 分别安装和升级包。

# R for Everyone

## package

### 通过 GitHub 直接安装包

```
require(devtools)
install_github(rep = "coefplot", username = "jaredlander")
```

### 加载包，不提示

```
require(coefplot, quietly = TRUE)
```

### 卸载包

```
detach("package:coefplot")
```

同名包用 `::`

## R 基础

+ 类似 Python 的界面，可直接做运算
+ 变量赋值 `x <- 2; y = 5; assign("j", 4)`
+ 移除变量 `rm(j)`。还有垃圾收集命令 gc。
+ 类型检测 `is.numeric(); is.integer()`
+ 字符长度 `nchar()`，也可用于向量。
+ 时间操作 `as.Date(""); as.numeric(); as.POSIXct("")`，另有包 lubridate 和 chron。
+ 逻辑类就是布尔类。
+ 向量长度 `length(vec)`，逻辑判断 `any(); all()`
+ 初始化时即可给向量的每个元素一个名称，以类似字典的形式。或者给 `names(vec)` 赋值名称向量。
+ factor 向量 `as.factor(vec)`。factor 有 level，即其唯一元素集合。技术上，R 给了每个唯一值一个整数，可用 `as.numeric(factor_vec)` 看到。
+ `factor()` 有参数 x, leveles, ordered。ordered 如果为 TRUE，则创建的 factor 有顺序，在弄等级的时候这个很有用。
+ `?\`\`` 看帮助，在不知道全名的情况下找函数 `apropos("")`
+ `is.na(); is.null()`

## 高级数据结构

+ `data.frame(vec1, vec2, ...)` 创建 data.frame，每个向量一列，列名默认为向量的变量名。也可以给出字典的形式，那么等号前面的就是列名。
+ 维度 `nrow(); ncol(); dim()`，列名 `names()[]`，行名称（默认为数字字符） `rownames()`，可以给其赋向量值。如果赋值为 NULL，则变回默认的数字。
+ `head(), tail()` 显示部分数据，有参数 n。
+ 用 $ 访问单个列，可返回 factor。可用中括号访问单个元素，行、列用逗号隔开。可以有 : 构成的 slice。逗号的一边可以为空。中括号中可以用列名。如果只有一个列名且不用逗号，返回简单的列信息。因为只用一对中括号的 class 不是 factor；用两对中括号是的。中括号有 drop 参数。
+ `model.matrix()` 可以将 factor 以矩阵的形式显示，值为 0 或 1。
+ `list()` 括号中有几个参数，构成的 list 就有几个部分。也可用 `names()` 给各元素赋值。可用 `vector(mode = "list", length = *)` 来创建指定长度的空列表。可用双中括号访问列表元素，但是每次只能访问一个。可用数字也可用字符名称索引。而通过此法得到单个元素后，就可以再用之前的方法访问子元素。
+ 矩阵可用 `matrix()` 创建，参数有元素向量、nrow。`rownames(), colnames()` 可对矩阵的行列名称进行操作。矩阵转置（`t()`）后，行列名称也一样转置。
+ `array()` 函数创建数组，要有数据向量参数，可有参数 `dim`。如果数据向量的长度不够，会循环使用。但是对已有元素的向量调用总长不符的 `dim` 函数，会出错。dim 的向量参数第一个元素是代表行索引，第二个是列索引，之后的是靠外部的索引。

## 读入数据

+ `read.table()` 可以从 CSV 文件中读入数据，返回值是 data.frame。`tomato <- read.table(file = url, header = TRUE, sep = ",")`
+ 还有一个参数 `stringAsFactors`，默认为真，将其设为假可以防止将字符串列转换成 factor。这样可以节约计算时间，而且让列保持为字符串也便于操作。此参数还可用于 `data.frame()`。
+ `read.table()` 的另外两个有用的参数，`quote` 和 `colClasses`，分别表示包围单元格的字符和每个列的数据类型。
+ 如果 CSV 的质量很差，可换用 `read.csv2(), read.delim2()`。
+ 连接数据库：`require(RODBC); db <- odbcConnect("")`
+ 数据库查询：`table <- sqlQuery(db, "sql command", stringAsFactors = FALSE)`
+ 在用完后最好调用 `odbcCloce()`
+ foreign 包提供了读取许多其他软件数据的函数。
+ RData 文件，是可以表示任何种类的 R 对象的二进制文件，可以在多个平台间传递。`save()` 可以把对象存储成 .rdata 文件，参数有 file，指示文件路径和名称。之后可用 `load()` 载入。
+ 内置数据集目录可用 `data()` 查看，以名称为参数则可载入数据。给定 `package` 参数，则可以从特定的包中获取数据。如 `data(diamonds)`
+ XML 包中有个 `readHTMLTable()` 函数可用来抓取 HTML 表格。

## 统计图形

+ `hist(diamonds$carat, main = "Carat Histogram", xlab = "Carat")` main 参数是图形的标题
+ `plot(price ~ carat, data = diamonds)` 画的是点图。~ 表示我们要看 price 因为 carat 变化的情况，后者是 x 值、前者是 y 值。不用 formula 接口形式：`plot(diamonds$carat, diamonds$price)`
+ `boxplot(diamonds$carat)` 其思想是粗实线代表中点，盒子则将中间 50% 的数据包含在内。四分位点，就是把所有点分成 4 分的点，中间是中点 Q2，两边再分中点，分别是 Q1 和 Q3。IQR = Q3 - Q1。而为了防止 outlier，设置 Lower fence = Q1 - 1.5 x IQR, Upper fence = Q3 + 1.5 x IQR。
