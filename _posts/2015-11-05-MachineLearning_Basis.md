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

### Neural Network

![activation]({{url.site}}/assets/20151105/activation.png)      表示第j层，第 i 个神经元的输入激励

![Theta]({{url.site}}/assets/20151105/Theta.png)    表示weights矩阵，从 j 到 j+1 层的隐射关系 ![ThetaSize]({{url.site}}/assets/20151105/ThetaSize.png)

![Thetaij]({{url.site}}/assets/20151105/Thetaij.png)    表示从 j 层所有神经元到 j+1 层的第 i 个神经元，对应的参数；即![Theta]({{url.site}}/assets/20151105/Theta.png) 中第i行为 j 层到 j+1 层的第 i 个神经元，需要的 s{j}+1 个参数，j+1层总共有 s{j+1}个神经元

![connection]({{url.site}}/assets/20151105/connection.png) 表示 j+1 层与 j 层之间的连接关系

![a21]({{url.site}}/assets/20151105/a21.png)

![a22]({{url.site}}/assets/20151105/a22.png)

![a22]({{url.site}}/assets/20151105/a23.png)

![a31]({{url.site}}/assets/20151105/a31.png)

![x]({{url.site}}/assets/20151105/x.png) <4x1>

![z2]({{url.site}}/assets/20151105/z2.png) <3x1>

![a2]({{url.site}}/assets/20151105/a2.png) <3x1>

![z2_computation]({{url.site}}/assets/20151105/z2_computation.png)  <3x4> x <4x1> = <3x1>

![a2_computation]({{url.site}}/assets/20151105/a2_computation.png) <3x1> = <3x1>

![z3]({{url.site}}/assets/20151105/z3.png) <1x4> x <1+3x1> = <1x1>

![a3]({{url.site}}/assets/20151105/a3.png) <1x1>

![nncost]({{url.site}}/assets/20151105/nncost.png) 其中h(x)<kx1>，h(x){i}表示输出<kx1>的第i个输出值；对K的求和，表示k个输出单元的求和；yi{k}表示第i个样本的第k个值，为数值（0或1），h{xi}{k}表示第i个样本，在输出层的第k个神经元的输出，为数值（0或1）；sum{k}表示一个样本在输出层上的误差

![nnJ]({{url.site}}/assets/20151105/nnJ.png)     表示neural network中，加了正则项的cost function

![delta]({{url.site}}/assets/20151105/delta.png)   表示第 l 层上第 j 个节点的误差error

### NN example 

![nn]({{url.site}}/assets/20151105/nn.png)     表示四层neural network

![Theta_lij]({{url.site}}/assets/20151105/Theta_lij.png)  表示正向pass中，在 l 层上，第 j 个神经元对应，l+1层上，第 i 个神经元的权值系数

![Theta_lijT]({{url.site}}/assets/20151105/Theta_lijT.png)   表示反向pass中，在 l+1 层上，第 i 个神经元对应，l 层上第 j 个神经元

![a_1]({{url.site}}/assets/20151105/a_1.png)  <4X1>

![z_2]({{url.site}}/assets/20151105/z_2.png)  Theta1<5x4> a1<4x1> = z2<5x1>

![a_2]({{url.site}}/assets/20151105/a_2.png)  a2<6x1> 增加a2{0}

![z_3]({{url.site}}/assets/20151105/z_3.png)   Theta2<5x6> a2<6x1> = z3<5x1>

![a_3]({{url.site}}/assets/20151105/a_3.png)   a3<6x1> 增加a3{0}

![z_4]({{url.site}}/assets/20151105/z_4.png)    Theta3<4x6> a3<6x1> = z4<4x1>

![a_4]({{url.site}}/assets/20151105/a_4.png)    a4<6x1>

![deltaj]({{url.site}}/assets/20151105/deltaj.png) 

![delta4]({{url.site}}/assets/20151105/delta4.png)   <4x1> 

![delta3]({{url.site}}/assets/20151105/delta3.png)<6x1>    Theta3{T}<6x4> delta4<4x1> a3<6x1> (1-a3) <6x1>      （根据连接关系，反向推导delta3，参考Week5 Cost Function and Backpropagation）
（上述公式与下面矩阵就J(Theta)公式相似，只不过增加了对激励函数求导的计算）

![delta2]({{url.site}}/assets/20151105/delta2.png)<6x1>    Theta2{T}<6x5> delta3<5x1> （由于delta3计算了bias，但是bias只被计算，不参加反向。因此delta3由<6x1>变为<5x1>） a3<6x1> (1-a3) <6x1> 

第一层为输入层，只是观察使用，不使用误差计算

![partial]({{url.site}}/assets/20151105/partial.png)   <s{j+1} x s{j}+1> delta{l+1}<(s{j+1}) x 1> a{l}<1 x s{j}+1>

![Delta]({{url.site}}/assets/20151105/Delta.png)  <s{l+1} x s{l}+1>   这里一个Delata代表一个样本，相加表示对所有m个样本计算总梯度

![Dij]({{url.site}}/assets/20151105/Dij.png) <s{l+1} x s{l}+1>  这里Delta除以m，表示求m个样本的平均梯度，lambda表示正则项的约束

（对于单个样本，且不计算正则化的情况下，网络梯度为![singlesample]({{url.site}}/assets/20151105/singlesample.png)）

![partial_3]({{url.site}}/assets/20151105/partial_3.png) <4x6> delta4<4x1> a3T<1x6> （可用矩阵行列乘法，理解其计算意义）

![D_3]({{url.site}}/assets/20151105/D_3.png)  <4x6>   3到4层连接的样本平均梯度（可忽略正则项）

![partial_2]({{url.site}}/assets/20151105/partial_2.png) <5x6> delta3<5x1>(bias不参与反向传播，减1个) a2T<1x6>

![D_2]({{url.site}}/assets/20151105/D_2.png)   <5x6>   2到3层连接的样本平均梯度

![partial_1]({{url.site}}/assets/20151105/partial_1.png) <5x4> delta2<5x1>(bias不参与反向传播，减1个) a1T<1x4>

![D_1]({{url.site}}/assets/20151105/D_1.png)    <5x4>   1到2层连接的样本平均梯度

![ThetaD]({{url.site}}/assets/20151105/ThetaD.png)    最终i梯度计算结果的表示

![update]({{url.site}}/assets/20151105/update.png)   更新连接weights计算

![comparision]({{url.site}}/assets/20151105/comparision.png)   先计算delta，计算误差<s{l} x 1>；再计算D梯度，使用之前计算的delta<s{l+1} x s{l}+1>