---
layout: post
title:  "论文解读《Visualizing and Understanding Convolutional Networks》"
date:   2015-11-01
categories: PaperReading
---

# PaperReading

## ABSTRACT

这篇论文主要讨论了为什么深度网络性能如此优越，与通过什么方式可以提升

## INTRODUCTION

从1989年开始，CNN就在手写体识别以及人脸识别方面有显著效果，近几年在更具有挑战性的视觉分类任务中，也表现出了突出的性能。特别是在ILSRVC2012上，有突出表现。重新使用卷积模型有几点原因：(i) 大量有样本标注的训练集 (ii) GPU性能可实现模型计算 (iii) 更好的正则化策略

进入有如此大的进步，却很少有对复杂模型的内部操作以及如何达到如此优越性能的研究。从科学的观点上看，是不令人满意的。不了解其如何以及为什么工作的，更好模型的发展也只是traial-and-error（不断摸索）。在这论文中，介绍了视觉技术，来表现在模型的任意层，输入刺激形成的feature map。其让我们可以观察，训练时feature的演化，分析模型的潜在问题。至于可视技术（visualization technique）用multi-layered Deconvolutional Network来将特征激励反向形成输入像素空间。另外，通过对输入图像的部分遮挡，我们也分析了一个分类器输出的敏感度分析，表明了对于分类，场景中哪一部分是重要的。

使用了这些工具，以AlexNet开始，讨论了不同网络，在ImageNet上的结果。随后，通过在softmax层的重新训练，探究了模型对不同数据集的泛化能力。