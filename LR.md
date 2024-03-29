## 逻辑回归
逻辑回归是一个分类算法，它可以处理二元分类以及多元分类。虽然它名字里面有“回归”两个字，却不是一个回归算法。
>https://www.cnblogs.com/pinard/p/6029432.html

## 1.几个要点
### （1）对数几率
- 一个事件发生的几率(odds)是指该事件发生的概率与该事件不发生的概率的比值。
- 在LR模型中，输出y=1的对数几率是输入x的线性函数，或者说y=1的对数几率是由输入x的线性函数表示的模型，即LR模型
### （2）函数映射
- LR本质上还是线性回归，只是特征到结果的映射过程中加了一层函数映射，即sigmoid函数，即先把特征线性求和，然后使用sigmoid函数将线性和约束至(0,1)之间，结果值用语二分或回归预测。
### （3）LR为什么用sigmoid函数。这个函数有什么优点和缺点？为什么不用其他函数？
- **为什么用sigmoid函数**
（1）取值范围在0~1之间。 
（2）对于一个事件发生情况，50%是其结果的分水岭，选择函数应该在0.5中心对称
（3）maximum entropy的性质。

## 2.LR的优缺点
### 优点
- 预测结果是界于0和1之间的概率；
- 可以适用于连续性和类别性自变量；
- 容易使用和解释；
### 缺点
- 对模型中自变量多重共线性较为敏感，例如两个高度相关自变量同时放入模型，可能导致较弱的一个自变量回归符号不符合预期，符号被扭转。​需要利用因子分析或者变量聚类分析等手段来选择代表性的自变量，以减少候选变量之间的相关性；
- 预测结果呈“S”型，因此从log(odds)向概率转化的过程是非线性的，在两端随着​log(odds)值的变化，概率变化很小，边际值太小，slope太小，而中间概率的变化很大，很敏感。 导致很多区间的变量变化对目标概率的影响没有区分度，无法确定阀值。

## 3.与SVM比较
### 与SVM的相同点
- LR与SVM都是分类算法
- LR与SVM都是有监督学习算法
- LR与SVM都是判别模型
- LR与SVM都是线性模型
### 与SVM的不同点
- **本质上的不同是损失函数的不同，LR的是log loss SVM的损失函数是hinge loss**
- **优化目标不同，LR的目标函数是logloss，SVM是最大化分类面间距**
(1) 逻辑回归方法基于概率理论，假设样本为1的概率可以用sigmoid函数来表示，然后通过极大似然估计的方法估计出参数的值，具体细节参考http://blog.csdn.net/pakko/article/details/37878837。
(2) 支持向量机​基于几何间隔最大化原理，认为存在最大几何间隔的分类面为最优分类面，具体细节参考>http://blog.csdn.net/macyang/article/details/38782399
- **SVM考虑局部（支持向量），而LR考虑全局**
(1) LR侧重于所有点，SVM侧重于超平面边缘的点
(2) 线性SVM不直接依赖于数据分布，分类平面不受一类点影响；LR则受所有数据点的影响，如果数据不同类别strongly unbalance，一般需要先对数据做balancing。
- **在解决非线性问题时，支持向量机采用核函数的机制，而LR通常不采用核函数的方法**
(1) 在计算决策面时，SVM算法里只有少数几个代表支持向量的样本参与了计算，也就是只有少数几个样本需要参与核计算
(2) LR算法里，每个样本点都必须参与决策面的计算过程，也就是说，假设我们在LR里也运用核函数的原理，那么每个样本点都必须参与核计算，这带来的计算复杂度是相当高的
>所以，在具体应用时，LR很少运用核函数机制。LR主要靠特征构造，必须组合交叉特征，特征离散化。
- **线性SVM依赖数据表达的距离测度，所以需要对数据先做normalization（归一化），LR不受其影响**
因为Linear+SVM在计算margin有多“宽”的时候是依赖数据表达上的距离测度的，换句话说如果这个测度不好.所求得的所谓Large+margin就没有意义了，这个问题即使换用kernel+trick（比如用Gaussian+kernel）也无法完全避免。所以使用Linear+SVM之前一般都需要先对数据做normalization，而求解LR（without+regularization）时则不需要或者结果不敏感。
- **SVM自带正则化，LR必须额外添加**
这就是为什么SVM是结构风险最小化算法的原因
- **LR和SVM在实际应用的区别**
对于小规模数据集，SVM的效果要好于LR，但是大数据中，SVM的计算复杂度受到限制，而LR因为训练简单，可以在线训练

## 4.与线性回归的比较
1）线性回归要求变量服从正态分布，logistic回归对变量分布没有要求。 
2）线性回归要求因变量是连续性数值变量，而logistic回归要求因变量是分类型变量。 
3）线性回归要求自变量和因变量呈线性关系，而logistic回归不要求自变量和因变量呈线性关系 
4）logistic回归是分析因变量取某个值的概率与自变量的关系，而线性回归是直接分析因变量与自变量的关系