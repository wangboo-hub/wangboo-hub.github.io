---
title: 测试
authors: ad
priority: 10.08
---

# 测试


## STL  

### priority_queue

优先队列，默认是大根堆

#### 头文件

```cpp
#include<queue>
```

#### 操作

```cpp
//定义成小根堆的方式：
    priority_queue<int, vector<int>, greater<int>> q;
```

表达式 |意义
:--:|:--:
`size()`|返回容量大小
`empty()`|判断是否为空  
`push()`|插入一个元素
`top()`|返回堆顶元素
`pop()`|返回堆顶元素

### queue

队列
表达式 |意义
:--:|:--:
`size()`|返回容量大小
`empty()`|判断是否为空
`push()` |向队尾插入一个元素
`front()`|返回队头元素
`back()`|返回队尾元素
`pop()`|弹出队头元素

### set, map, multiset, multimap

基于平衡二叉树（红黑树），动态维护有序序列
    size()
    empty()
    clear()
    begin()/end()
    ++, -- 返回前驱和后继，时间复杂度 O(log2n)

#### set/multiset

表达式 |意义
:--:|:--:
`insert()`|插入一个数
`find()`|查找一个数
`count()`|返回某一个数的个数
`erase()`|(1) 输入是一个数x，删除所有x   O(k + log2n)<br>(2) 输入一个迭代器，删除这个迭代器
`lower_bound(x)`|返回大于等于x的最小的数的迭代器
`upper_bound(x)`|返回大于x的最小的数的迭代器

#### map/multimap

表达式 |意义
:--:|:--:
`insert()`|插入的数是一个pair
`erase()`|输入的参数是pair或者迭代器
`find()`|
`[]`|注意multimap不支持此操作。 时间复杂度是 O(log2n)
`lower_bound()/upper_bound()`|

unordered_set, unordered_map, unordered_multiset, unordered_multimap, 哈希表
和上面类似，增删改查的时间复杂度是 O(1)
不支持 lower_bound()/upper_bound()， 迭代器的++，--




## 研究技能入门

## 如何阅读文献

[阅读文献入门](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf)

## 如何写作

youtube 视频(如不能观看联系管理员给予建议)

<iframe width="800" height="600" src="//player.bilibili.com/player.html?aid=73708985&bvid=BV1TE411h7B9&cid=126075594&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

Whitesides教授的大作

Whitesides, G. M. Whitesides’ Group: Writing a Paper. *Adv. Mater.* **2004**, *16* (15 SPEC. ISS.), 1375–1377.

## 如何用英语演讲

[English for Presentations at International Conferences](https://book.douban.com/subject/25773106/)


## 如何归档/整理项目文件

## 数据整理的必要性

为了能让接收项目的人，以及组里其他人的数据能够相互参考，避免不必要的重复计算和浪费。我与云霈总结了一些简单的整理规则。

## 数据整理的规则

### 规则1

以项目名称命名大文件夹。例：SnO2110面的机器学习

```bash
SnO2110-ML #项目文件名
```

### 规则2

以**数字**作为目录名前缀，以下**划线命名法**来给目录命名。

因为计算必定伴随着**目的**，所以目录名以计算的**目的**来命名。

**数字**可以使目录按照自己的意志来排序，**下划线命名法**可以有效的阅读。例：

```bash
./SnO2110-ML
├── 00.train_set #放训练集
├── 01.train_set_test #做训练集测试
├── 02.DP_Pots #放机器学习势能
├── 03.dissociation #计算解离度
├── 04.surface_tension #计算表面张力
```

注意：再次一级目录可不按照以上方法来命名，尽量使用**下划线命名法**即可。

### 规则3

对于**作图类的目录**，要保留作图的**数据**，**原始脚本**和**作出来的图**。例：

```bash
01.train_set_test
├── TrainSetEnergy.pdf #作出来的图
├── TrainSetForce.png #作出来的图
├── TrainingSetError.py #处理作图的脚本 可以直接运行！
├── e.out #作图的原始数据
└── f.out #作图的原始数据
```

对于**计算类的目录**，要保留**必要的输出文件**和**输入文件**。例：

```bash
02.DP_Pots #放机器学习势能
├── v1.0 #版本号
│   ├── graph.000.pb #势能函数，输出文件的一种
│   ├── graph.001.pb
│   ├── graph.002.pb
│   ├── graph.003.pb
│   ├── input.000.json #对应的输入文件
│   ├── input.001.json
│   ├── input.002.json
│   └── input.003.json
├── v1.2
│   ├── graph.000.pb
│   ├── graph.001.pb
│   ├── graph.002.pb
│   ├── graph.003.pb
│   ├── input.000.json
│   ├── input.001.json
│   ├── input.002.json
│   └── input.003.json
└── v1.3
    ├── README
    ├── graph.000.pb
    ├── graph.001.pb
    ├── graph.002.pb
    └── graph.003.pb
```

### 规则4

在文件夹里放入必要的说明文件，例如**README**

```bash
└── v1.3
    ├── README #必要的说明文件，推荐使用markdown语言书写
    ├── graph.000.pb
    ├── graph.001.pb
    ├── graph.002.pb
    └── graph.003.pb
```

```markdown
# README
 converted from v1.2 pot
 compress input use that v1.2 training input
```
