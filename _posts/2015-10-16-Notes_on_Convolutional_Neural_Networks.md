---
layout: post
title:  "论文解读《Notes on Convolutional Neural Networks》"
date:   2015-10-16
categories: Paper
---

## Paper Reading

### Introduction

本文讨论了CNN的推导与实现，以及一些简单的拓展内容。CNN包含了很多比权值更多的连接个数；在框架上（architecture），它实现了正则化的一种形式。另外，CNN提供了一定程度的平移不变性（translation invariance）。这种特殊形式的神经网络，假设了我们需要学习用数据驱动的filter，作为一种提取描述输入的特征的方法。在此文的推导中，是用二维数据与卷积进行的，但是可以不需多余的代价，即可转化为任意维数的实现

在此，先进行全连接层的典型反向传播介绍，接着是在2D卷积层中，反向传播对filiter以及下采样（subsampling）层的更新。通过讨论，我们突出强调了实现的有效性，以及一小段Matlab代码来对应等式。随后，再讨论如何结合从之前的各层中的特征映射（feature maps）。

### Vanillar Back-propagation Through Fully Connected Networks

在典型的卷积神经网络中，早期的分析主要是改变convolution和sub-sampling操作，然而，框架（architecture）中最后部分是，多个1维的全连接层。但你想要将最后的2D feature map作为1D全连接层的输入，一个简便的做法便是将在输出map上的feature，转换为一个长的输入向量。分析CNN的算法前，先讨论标准的反向传播算法。

#### Feedforward Pass

推到公式中，使用平方误差损失函数（squared-error loss function）

![screenshot]({{ site.url }}/assets/squared-error_loss_function.jpg)
