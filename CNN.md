# 1.CNN 的基本特征
稀疏交互和参数共享
### 动机
- 局部特征——卷积的核心思想
- 平移等变性
### 意义
- 提高统计效率
当处理一张图像时，输入的图像可能包含成千上万个像素点，但是我们可以通过只占用几十到上百个像素点的核来检测一些局部但有意义的特征，例如图像的边缘。
- 减少参数数量
减少存储需求
加速计算

#2.为什么使用 CNN 代替 RNN
### RNN 与目前的硬件加速技术不匹配
训练 RNN 和 LSTM 非常困难，因为计算能力受到内存和带宽等的约束。简单来说，每个 LSTM 单元需要四个仿射变换，且每一个时间步都需要运行一次，这样的仿射变换会要求非常多的内存带宽。添加更多的计算单元很容易，但添加更多的内存带宽却很难
### RNN 容易发生梯度消失，包括 LSTM
在长期信息访问当前处理单元之前，需要按顺序地通过所有之前的单元。这意味着它很容易遭遇梯度消失问题；LSTM 一定程度上解决了这个问题，但 LSTM 网络中依然存在顺序访问的序列路径；实际上，现在这些路径甚至变得更加复杂
### 注意力机制模块（记忆模块）的应用
- 注意力机制模块可以同时前向预测和后向回顾。
- 分层注意力编码器
- 分层注意力模块通过一个层次结构将过去编码向量汇总到一个上下文向量
- 分层结构可以看做是一棵树，其路径长度为 logN