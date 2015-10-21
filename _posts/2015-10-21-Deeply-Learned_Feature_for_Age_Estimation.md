---
layout: post
title:  "论文解读《Deeply-Learned Feature for Age Estimation》"
date:   2015-10-21
categories: PaperReading
---

# PaperReading

## Abstract

人类年龄是人口统计的重要信息。与其他模式识别问题相比，年龄估计更具有挑战性，因为人脸图像对于年龄的差异变化不是很明显，而且每个人的年龄变化都不同。在这论文中，使用了基于CNN的深度学习技术用于年纪估计。建立了一种用于提取年龄特征，基于深度学习模型的方法。与之前的CNN模型，论文使用了从不同层中得到的feature map用来实现估计，而不是使用从top layer得到的feature。另外，还加入了一种流形的学习算法，很大程度上提升了性能。而且，用DLA（deep learned aging pattern）来评价分类与regression方案。这是第一次将深度学习技术使用在年龄估计的问题上。实验结果表明了，所提出的方法比state-of-the-art更好。

## Introduction

许多可视的，非语言信息是通过人脸进行传达的，包括身份，年龄，性别，种族以及情绪等。人脸在日常交流中非常关键。尽管基于图像的年龄估计具有实际应用，但是其仍然是很有挑战性的问题。通常有两个因素影响年龄进度。内在因素是有生理的因素，例如基因。外在因素包括生活环境，健康条件等。提取有效的年龄特征，不受个人因素的影响，仍是开放问题。

在这论文中，使用了新的框架，直接从数据中学习年龄特征。所学习到的特征比之前定义的特征提取算法更通用且具有分辨性。创新点：1. 提出了新的自动年龄估计的方法，是基于CNN的，首次将CNN用在年龄估计问题。2. 为了评将价提出的方案，比较了两个标准数据集的一些方法。实验结果表示，比state-of-the-art有明显提升。3. 使用了流形学习方法。而且，基于学习到的年龄特征，评价了不同个的回归和分类方法（regression and classification approach）

## Related Work

过去几年，有许多工作是基于年龄估计的学习的，主要分为两个部分：如何提取年龄特征，以及如何基于提取的特征预测年龄的。

## Proposed Approach

首先，提出CNN的基础，再讨论特征提取方法，主要关注学习到的特征是如果有效分辨年龄模式，以及在年龄估计问题上使用学习到的特征。然后，使用不同的流形学习方法，在低维度上获取潜在的年龄结构与表达年龄信息，提高性能。另外，还使用了不同的classification与regression方法，包括SVR，SVMs，PLS和CCA。

### Convolutional Neural Network

深度学习模型通过层次结果，提取不同层的特征。该结构可获分层的，抽象的，平移不变性的特征。从上述工作中，可以发现，深度学习适用于描述可视数据的高层次抽象特性，可组成多层非线性转换。CNN的结构是模仿人类视觉感觉的生物处理方式。在feature map中所学习的神经单元对应感知野的重叠区域。

CNN可用在计算机视觉，计入可视物体识别，检测和图像检索。CNN在从图像中提取特征具有好的能力。推测从更深的层中的学习的权值，对训练图像更有说服力。

#### Convolution Layers

在convolution层的每个神经元，由上一层的感受野与学习的权值，所组成的。在卷积后，是激励函数（activation function）：

![Convolution]({{url.site}}/assets/20151021/Convolution.png)

#### Sub-sampling Layers

下采样层是对给定的输入feature map进行下采样。只改变输入maps的尺寸，不改变map的数量。有许多中方式实现下采样：averaging，maximum或神经元连接。在这论文中，使用averaging。

#### Training Process

通常，训练CNN是为了最小化error function，对N个训练样本，重建的error function为

![ErrorFunction]({{url.site}}/assets/20151021/ErrorFunction.png)

上述error是对所有数据集进行计算的，是每个样本在各个神经错误的总和。

### Deep Learned Aging Pattern（DLA）

训练CNN模型实现多分类的年龄估计任务。网络由6层组成，输入2D的60x60像素的灰度人脸图像作为第一层的输入，kernel size为5x5。卷积后，在L2层的输入为56x56的feature map。在这层后，经过activation function（logistic function），得到feature map，然后经过pooling层。

L3为pooling层，size为2x2，pooling是用来滤波CNN的输出，对局部的平移和旋转更鲁棒。随后的L4为convolution，size为7x7。L5为pooling，L6由80个size为1x1的feature map组成。人脸图像是有标注的，用来实现监督学习的。

许多工作都在顶层作为特征表达。但是，与其他问题不同，在不同层对应特殊activations的表达，将这些提取的特征应用在预测年龄方面。

训练完CNN后，从不同层中提取特征，发现CNN的特征维数很高。高略到简单和有效性，通过PCA进行降维处理。PCA将X_{l}转化为Y_{l}，其中Y_{l}的维数较低。经过实验发现，PCA的使用几乎没有s使年龄估计发生改变。这一步在加速训练上，很有效。

流形方法（Mainfold）是为了提高性能，获取潜在脸部年龄结构。流形学习是实现保持样本维数不变，减少样本个数的方法。使用了MFA，OLPP和LSDA。

###     Regression or Classification

年龄估计可认为了回归问题，因为每个年龄都可以是一个回归至。同时，年龄估计也可以是分类问题，每个年龄作为一个类别标号。在这论文中，两者都使用且评价，用SVMs作为年龄分类，SVR作为年龄回归。

## Experiments

为了评价性能，这里使用了两种不同的评价方法，MAE和CS

### Datasets and Experimental Settings

论文中，为了比较state-of-the-art方法与评价所提出的方法，实验在两种公开的数据集上进行，MORPH与FG-NET。

在MORPH数据集中，将整个数据集分为两个部分，80%用来训练，20%用来测试。对于FG-NET数据集，使用LOPO设置。

![Dataset]({{url.site}}/assets/20151021/Dataset.png)

### Experimental Results and Analysis

![Method]({{url.site}}/assets/20151021/Method.png)

使用三种不同的流形学习算法，生成可分辨年龄模式的框架。其证明对新的数据集也有很好的效果。实验使用的回归方法为SVR。另一个实验了验证流形算法的有效性。

为了分析DLA中，不同分类和回归算法在MORPH上进行。分类和回归算法包括SVMs，SVR，PLS和CCA。
