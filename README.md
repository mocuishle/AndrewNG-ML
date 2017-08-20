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



