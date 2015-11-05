---
layout: post
title:  "Machine Learning 基础公式"
date:   2015-11-05
categories: DeepLearnig
---

# Machine Learning 基础公式

## Model and Representation

![sample]({{url.site}}/assets/20151105/sample.png)        表示第i个样本

![xfeature]({{url.site}}/assets/20151105/x_feature.png)    表示第i个样本中，x的n个特征

![theta]({{url.site}}/assets/20151105/theta.png)    表示模型的参数

![hypothesis]({{url.site}}/assets/20151105/hypothesis.png)        表示hypothesis对样本的预测结果

![error]({{url.site}}/assets/20151105/error.png)        表示对第i个样本的预测值与实际结果的误差，h与y都为一数值，二分类   非0即1

![cost]({{url.site}}/assets/20151105/cost.png)         表示预测结果与实际结果的cost，为数值

![derivation]({{url.site}}/assets/20151105/derivation.png)         表示对第j个参数求导，直到收敛；用上一周期的参数，一次性更行所有参数，非用最新值更新本次参数

![derivation_theta]({{url.site}}/assets/20151105/derivation_theta.png) 表示对cost function的theta计算

## Logical Regression

![logistic_hypothesis]({{url.site}}/assets/20151105/logistic_hypothesis.png)    表示对logistic regression的hypothesis公式，输出一个数值（0或1）

![cost_logistic]({{url.site}}/assets/20151105/cost_logistic.png)    表示对不同的y时，cost的表示

![logistic_regression]({{url.site}}/assets/20151105/logistic_regression.png)    表示统一的logistic regression cost function，y{i}为{0,1}，y{i}<1x1>，thetaT<1xn>，x{i}<nx1>，thetaT<1xn>*x{i}<nx1>=h_theta<1x1>

## Multiclass classification

![multi_hypothesis]({{url.site}}/assets/20151105/multi_hypothesis.png)    表示对特定的x与theta，对样本分类，预测样本属于i类的概率

## Regularization

![regularization]({{url.site}}/assets/20151105/regularization.png)    表示对theta1-thetan进行限制，不包括theta0

### Regularized linear regression

![regularization]({{url.site}}/assets/20151105/regularization.png)    表示线性回归的正则化的使用

![theta0]({{url.site}}/assets/20151105/theta0.png)    表示求梯度时，对theta0求导，由于其不使用正则化，因此保持不变

![linear_gradient]({{url.site}}/assets/20151105/linear_gradient.png)    表示线性回归求导，其中x{j}(i)表示第i个样本中，第j维特征，不包含正则化

![regularization_gradient]({{url.site}}/assets/20151105/regularization_gradient.png)    表示用正则化后的J，求导

![thetaj]({{url.site}}/assets/20151105/thetaj.png)    表示首项中，thetaj参数<1，则thetaj变小，其影响值也小，而第二项与上式一致，则降低了thetaj，使某些thetaj不起作用

### Regularized logistic regression

![regularization_logistic]({{url.site}}/assets/20151105/regularization_logistic.png)    表示逻辑回归中，正则化对Cost的约束

![theta0]({{url.site}}/assets/20151105/theta0.png)    表示求梯度时，对theta0求导，由于其不使用正则化，因此保持不变

![linear_gradient]({{url.site}}/assets/20151105/linear_gradient.png)    表示逻辑    回归求导，其中x{j}(i)表示第i个样本中，第j维特征，不包含正则化

![regularization_gradient]({{url.site}}/assets/20151105/regularization_gradient.png)    表示用正则化后的J，求导。上述三个相似，但是由于![hypothesis_logistic]({{url.site}}/assets/20151105/hypothesis_logistic.png)，这为主要不同之处