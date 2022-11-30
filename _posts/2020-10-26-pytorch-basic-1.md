---
title: PyTorch基础（张量）
date: 2020-10-26 15:22:19 +0800
categories: [Tutorial, Coding]
tags: [python, deep learning]
math: true
---

本文主要记录自己学习 PyTorch 过程中涉及的一些基础知识。

<!--more-->

---
- [1. 张量维度](#1-张量维度)
  - [1.1. shape 属性](#11-shape-属性)
  - [1.2. size() 成员函数](#12-size-成员函数)
- [2. 张量比较](#2-张量比较)
  - [2.1. max](#21-max)
- [3. 参考文献](#3-参考文献)

# 1. 张量维度

## 1.1. shape 属性

输入

```python
import torch
# dim=2,shape=[2,3],随机生成Tensor
a = torch.FloatTensor(2, 3)
print(a.shape)
print(a.shape[0])
print(a.shape[1])
```

输出为

```python
torch.Size([2, 3])
2
3
```

## 1.2. size() 成员函数
输入

```python
import torch
# dim=2,shape=[2,3],随机生成Tensor
a = torch.FloatTensor(2, 3)
print(a.size())
print(a.size(0))
print(a.size(1))
```

输出为

```python
torch.Size([2, 3])
2
3
```

# 2. 张量比较

## 2.1. max

不指定维度时，返回一个张量，为输入数据中的最大值

```python
>>> a = torch.randn(1, 3)
>>> a
    tensor([[ 0.6763,  0.7445, -2.2369]])
>>> torch.max(a)
    tensor(0.7445)
```

指定维度时，返回一个 tuple，包含沿着该维度的最大值和对应的序号。

```python
>>> a = torch.randn(4, 4)
>>> a
tensor([[-1.2360, -0.2942, -0.1222,  0.8475],
        [ 1.1949, -1.1127, -2.2379, -0.6702],
        [ 1.5717, -0.9207,  0.1297, -1.8768],
        [-0.6172,  1.0036, -0.6060, -0.2432]])
>>> torch.max(a, dim=1)
torch.return_types.max(values=tensor([0.8475, 1.1949, 1.5717, 1.0036]), indices=tensor([3, 0, 0, 1]))
```
对于二维张量，`dim=0` 沿列求最大（跨行间比较），`dim=1` 沿行求最大（跨列间比较）。

对于三维张量，构成为 `(通道，行，列)`，那么`dim=0` 通道间比较求最大，`dim=1` 跨行间比较求最大，`dim=2` 跨列间比较求最大。

```python

import torch
 
a = torch.randn(2,3,4) #随机生成数组
max_0=torch.max(a,dim=0) #针对第1个元素“2”，对应的是通道
max_1=torch.max(a,dim=1) #针对第2个元素“3”，对应的是行
max_2=torch.max(a,dim=2) #针对第2个元素“4”，对应的是列
print("a:\n", a)
print("************************************************")
print("max(a)_0:", max_0)  #dim=0,通道间进行比较，所以返回每一张特征图，同一像素位置上的最大值
print("max(a)_1:", max_1)  #dim=1，行与行之间进行比较，所以返回每一张特征图，每一列的最大值
print("max(a)_2:", max_2)  #dim=2，列与列之间进行比较，所以返回每一张特征图，每一行的最大值
 
<<
a:
 tensor([[[ 0.5323,  1.5229, -0.6122,  0.6054],
         [ 1.2424, -1.6005,  0.0779,  0.9227],
         [-0.6340, -0.5770, -0.1672,  0.3598]],
 
        [[-0.3770, -0.4992,  1.8444, -1.1040],
         [ 1.2238,  0.7283, -1.6462,  0.0325],
         [-0.3555, -0.2599,  1.5741,  1.0683]]])
************************************************
max(a)_0: (tensor([[ 0.5323,  1.5229,  1.8444,  0.6054],
        [ 1.2424,  0.7283,  0.0779,  0.9227],
        [-0.3555, -0.2599,  1.5741,  1.0683]]), tensor([[ 0,  0,  1,  0],
        [ 0,  1,  0,  0],
        [ 1,  1,  1,  1]]))
max(a)_1: (tensor([[ 1.2424,  1.5229,  0.0779,  0.9227],
        [ 1.2238,  0.7283,  1.8444,  1.0683]]), tensor([[ 1,  0,  1,  1],
        [ 1,  1,  0,  2]]))
max(a)_2: (tensor([[ 1.2424,  1.5229,  0.0779,  0.9227],
        [ 1.2238,  0.7283,  1.8444,  1.0683]]), tensor([[ 1,  0,  1,  1],
```

也就是说，`dim` 参数是按照张量维度从左到右、从外到内的顺序进行比较的。

# 3. 参考文献

[1] [梦并不遥远](https://www.cnblogs.com/zyg123/). [4.3Python数据处理篇之Matplotlib系列(三)---plt.plot()](https://www.cnblogs.com/zyg123/p/10504633.html).

[2] [我的明天不是梦](https://www.cnblogs.com/xiaoboge/). [python使用matplotlib:subplot绘制多个子图](https://www.cnblogs.com/xiaoboge/p/9683056.html).