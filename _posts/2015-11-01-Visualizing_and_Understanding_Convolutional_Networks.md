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

使用了这些工具，以AlexNet开始，讨论了不同网络，在ImageNet上的结果。随后，通过在softmax层的重新训练，探究了模型对不同数据集的泛化能力。与其他无监督的预训练相比，这是有监督的预训练。

## Approach

轮种使用了标准的完全监督卷积网络，LeNet和AlexNet。

## Visualization with a Deconvnet

论文提出了一种新颖的方法，将中间层的feature activities反向匹配到输入像素空间(map these activities back to the input pixel space)，表明了原始输入模型在feature map上所产生的activation。一个deconvenet可以使用用相同的部件（filtering, pooling），只不过是起反作用，将features匹配到像素。

为了检查一个convnet，deconvnet被连接到每一层上，提供了返回图像像素的路径。以输入图像和每层计算的特征开始。威力检查convnet激励，将其他激励置0，输入feature maps进相连的deconvnet层中。随后经过unpool，rectify（修正）和filter来重建每层的activity。不断重复知道像素空间恢复。

Unpooling：convnet中，max pooling操作不可逆，然而可以通过在pooling区域使用switch变量，记录最大值的位置得到反向估计值。在deconvnet中，unpooling操作通过使用从上层得到的这些switch，将重建放置在大概位置，保持激励的结构性。

Rectification：convnet使用relu non-linearities修正feature map，确保feature map都是正值。为了在每层得到有效的feature重建，将重建信号也通过一个relu non-linearity。

Filtering：convnet使用学习的fitler来卷积（convolve）之前层的feature map。为了求逆，deconvnet使用同样filter移位后的结果，引用在rectified map上，而不是这层的输出。这表示对每个fliter在水平和垂直方向就镜像。

由于模型是有辨识性地训练，其暗示性地表明了输入图像哪一部分是有辨识性的。这些预测不是模型的样本，因为这有生成性的过程在其中。

## Training Details

现在讨论在section.4的convnet模型，与AlexNet唯一不同就是在3，4，5层的sparse connection被替换成了dense connection。模型在ImageNet 2012的训练集，每张图像被resize为256，cropping 256x256的中心区域，substracting每个像素的mean。Stochastic gradient descent 用128的mini-batch来升级参数，用0.01的learning rate，用momentum为0.9。手动的降低learning rate当验证集错误率不变时。Dropout使用了0.5。所有权值初始为0.01，bias为0。

## Convnet Visualization

用Section 3所说明的模型，在ImageNet验证集上使用deconvnet来可视化feature activation。

Feature Visualization：当训练完成，图2表明了模型中的可视特征。不是使用一个最强的激励，论文显示了最好的9个激励。在像素空间上单独显示，不同结构刺激一个feature map，因此表现了输入变形的不变性。在这些feature visualization旁放置了相对应的图像patches。图像patches比visualization有更好的variation，因为后者在每个patch中值注重有辨识度的结构。例如，在layer5，第1行与第2列，patches几乎不相同，但是visualization表示特定的feature map关注背景里的草地，而不是前景物体。

每一层的输出，表明了在网络中特征的分层特性。Layer2对应边角与边缘的连接。Layer3有更赴藏的不变性，获取相似的纹理。Layer4显示了重要的变化，但是有更加细化的分别：狗脸与鸟腿。Layer5展示了重要的pose差异。