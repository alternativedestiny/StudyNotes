# Keras 学习笔记

## 核心层

1. 全连接层：神经网络中最常用的，实现对神经网络里的神经元激活

   ```python
   # units：全连接层输出的维度，即下一层神经元的个数
   # activation：激活函数，默认使用 Relu
   # use_bias：是否使用 bias 偏置
   Dense(units, activation='relu', use_base=True)
   ```

   

2. 激活层：对上一层的

   ```python
   # 激活函数，relu、tanh、sigmoid等
   Activation(activation)
   ```

3. Dropout层：对上一层的神经元随机选取一定比例的失活，不更新，但是权重仍然保留，防止过拟合

   ```python
   # rate：失活比例，0-1浮点数
   Droupout(rate)
   ```

4. Flatten层：将一个维度大于或等于3的高维矩阵，“压扁”为一个二维矩阵。即保留第一个维度（如：batch的个数），然后将剩下维度的值相乘作为“压扁”矩阵的第二个维度

   ```python
   Flatten()
   ```

5. Reshape层：将输入的维度重构成特定的shape

   ```python
   # target_shape：目标矩阵的维度，不包含batch样本数
   Reshape(target_shape)
   ```

6. 卷积层：卷积操作分为一维、二维、三维，分别为Conv1D、Conv2D、Conv3D。一维卷积主要应用于以时间序列数据或文本数据，二维卷积通常应用于图像数据。由于这三种的使用和参数都基本相同，所以主要以处理图像数据的Conv2D进行说明

   ```python
   # filters：卷积核的个数
   Conv2D(filters, kernel_size, strides=(1, 1), padding='valid')
   ```

## 备注

- [Keras入门](http://www.tensorflownews.com/2018/03/15/%e4%bd%bf%e7%94%a8keras%e8%bf%9b%e8%a1%8c%e6%b7%b1%e5%ba%a6%e5%ad%a6%e4%b9%a0%ef%bc%9a%ef%bc%88%e4%b8%80%ef%bc%89keras-%e5%85%a5%e9%97%a8/)
