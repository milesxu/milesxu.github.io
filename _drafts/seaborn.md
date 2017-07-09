layout: post
title: seaborn 函数库笔记
categories:
- Data Science
- seaborn
---

# `seaborn.FacetGrid`

生成子图网格，按照条件关联进行绘图。   
`FacetGrid`是一个对象，用来连接Pandas的`DataFrame`实例到matplotlib的具有特定结构的图。   
`FacetGrid`尤其可用于绘制具有多个子图，每个子图显示同样的关联，处在某些变量的不同级别的条件下的状态。可以指定最多三个条件变量，分别分派给网格的行、列以及子图元素的颜色。   
基本的流程是先利用数据集和构造网格的变量初始化`FacetGrid`类，然后通过调用`FacetGrid.map()`或者`FacetGrid.map_dataframe()`将一个或多个绘图函数应用于每个子集，最后可对子图元素进行微调。   
[文档链接](http://seaborn.pydata.org/generated/seaborn.FacetGrid.html)
