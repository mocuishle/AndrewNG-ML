

## About the course & author

Please see the [coursera](https://www.coursera.org/learn/machine-learning/home/info/README.md)
Taught by [Andrew Ng](https://www.coursera.org/instructor/andrewng/README.md)

## EX1
单变量、多变量的线性回归（有监督）：梯度下降  常规线性变换（Normal Equation）


### 梯度下降

1.选择预测方程类型（目前是线性），设置初始参数，并根据观测数据对变量进行归一化

2.根据MSE，计算出代价方程，并设置学习速率参数和迭代次数

3.根据预测方程、初始参数、观测数据、代价方程，对参数进行更新（参数更新方程）

4.根据代价方程降低速度，调整学习速率参数，直至迭代出代价方程最低值，并选择对应参数作为最终结果

### Normal Equation

原理 ： 将预测方程两端与变量的转置矩阵相乘，求解可得残差最小时的参数值。

需要注意：
    
        变量矩阵的內吉不可逆有两种情况 ：重复的特征（例如面积用英尺表达和用米表达作为两个特征）或特征过多
        
        解决：去掉部分特征，或者对变量进行正则化


## EX2
分类算法、Logistics回归分析、正则化应用

### 分类算法

将目标输出值离散化，并与对应的结果相映射。需要引用sigmoid函数来让预测的函数能够连续（方便后续观察、计算），具体形式 y=1/（1+e^(theta'*X)

预测函数依旧为连续函数，输出值可以看作样本为正例的概率大小

### Logistics回归

预测函数涉及到对数概率的操作，因此需要用Logistics回归来进行分析

原理：最大似然估计（MLE），略（后续会涉及到。。。）
回归方法：依旧是 梯度下降 和 Normal Equation（与线性回归最大的区别就是预测函数的形式有所变化，更新函数和代价函数也发生相应的变化）

### 正则化

如之前所说，引入过多的特征变量，会导致过耦合，正则化则是要减弱耦合的情况

正则化代价函数 = 原代价函数 + 正则参数*(theta.*theta)/（2*m）；

正则化代价函数最小化时兼顾了预测准确性和参数值的大小，后续参数值越小耦合程度会越低

## EX3

### 多个分类任务下的logistics回归

方法： one vs all，一次迭代选择一个分类作为正例

回归过程：与单一分类任务回归过程基本一致。

（与单一回归）差别 ：向量除了原来的维度之外还要考虑预测值向量的维度，在计算过程中要重视

### 利用神经网络分析手写数字

原理：模拟人体神经系统，根据阈值和非线性分类器来处理复杂的问题

优点：可以解决很多线性回归不能处理的非线性情况（例如异或），特征数量过多时

相关概念 ：输入层、隐藏层、输出层，权值网络，偏置神经元

建立过程 ：前向传播（暂时接触到这种），向量化运算

EX描述 ： 识别手写数字。根据像素区块的灰度来进行判断，但问题在于将每个区块作为输入变量值，变量数过多，计算量过于巨大。通过引入神经网络算法，将问题简化为多分类问题。sigmoid函数相当于感知器，将纷繁的样本变量简化为0~1的数值，并进行学习，若与观测值有偏差，则通过神经网络对权重和偏移量根据代价函数进行调整，直至符合预期。人为可以对学习过程进行干预，而学得的结果和网络模型则是由机器搞定。

EX3 比较简单，参数均已设置好，只需按照前向传播搭建网络即可

## EX4
梯度校验、后向传播、代价函数、随机化初始参数

### 代价函数
按照前向传播过程计算，与线性回归、logistics回归基本相同，但与多分类回归相似需要考虑预测值向量维度，且正则化过程也有所不同，参数部分的计算与其在网络中的层级相对应

### 后向传播
根据观测值，对神经网络进行调整，需要两个输出结果 ：代价函数 和 其偏导（用于对权重网络进行更新）。

由于前向传播的神经网络特性，无法具体检测所有输出层在某一次输入时的输出，但依旧需要根据各个位置的残差来计算其对应参数需要调整的幅度，即代价函数在各个位置的偏导（每个输出单元所在位置和权重都有所不同）。

根据在最终输出端得到的与预期的差值，推算出上一层输出单元的差值，从而将权重、位置关系等因素囊括进来，进而让参数更为准确的调整。这个过程就叫做后向传播，主要是用于更新参数，从而迭代降低J

此外，初始参数设置要尽量随机化，不能像之前一样全设置为0或1，因为对称的参数会使得迭代出的每一层基本都相同，而无法继续计算。对称的初始参数相当于让神经网络变成之前的线性回归，求解得到的只是一个线性方程。

### 梯度校验
原理 ：曲线上位置相近的两点之间直线的斜率与该处导数值相等（相似）
用途 ：复杂的神经网络计算较为复杂且周期很长，需要在前期确定是否有代码错误、计算公式错误。梯度校验可以在计算参数更新值时即可进行检测，较早的排除非受迫性失误

需要注意的是，检验无问题后，需要在迭代前关闭梯度检验的相关代码，否则会较大增加运算负担。

EX4 依旧是针对EX3中的识别问题，不过需要通过自己设置的后向传播网络计算参数值，根据J函数曲线变化，设置对应的学习速率和迭代次数。由于J函数不是凸函数，因此我们得到的结果很可能是局部优化的结果。Andrew在octave里给了一个自己写的优化参数的函数 fmincg，用这个可以求出最优化的参数，原理与octave自带的fminun基本一致
