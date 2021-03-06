
前言：如果我们使用的模型很简单（比如逻辑回归LR），我们通常会把连续型的特征转换为离散型的特征，然后再对离散型的特征进行one-hot 编码或者哑编码。这样会使我们的模型具有很强的非线性能力。

### one-hot编码

解释：将离散特征的每一种状态都看成是一种状态，保证每一种取值只保证一种状态处于激活态，其他状态位都为0。

### 哑编码

解释：将任意一个状态位去除

**总结：我们使用one-hot编码时，通常我们的模型不加bias项 或者 加上bias项然后使用![img](https://images2017.cnblogs.com/blog/1251096/201711/1251096-20171104162333248-539020480.png)正则化手段去约束参数；当我们使用哑变量编码时，通常我们的模型都会加bias项，因为不加bias项会导致固有属性的丢失**。

选择建议：我感觉最好是选择**正则化 + one-hot编码**；哑变量编码也可以使用，不过最好选择前者。虽然哑变量可以去除one-hot编码的冗余信息，但是因为每个离散型特征各个取值的地位都是对等的，随意取舍未免来的太随意。

### 连续值的离散化为什么会提升模型的非线性能力？

 　简单的说，使用连续变量的LR模型，模型表示为公式（1），而使用了one-hot或哑变量编码后的模型表示为公式（2）

　　　　　![img](https://images2017.cnblogs.com/blog/1251096/201711/1251096-20171106165501794-386583892.png)

式中$x_1$表示连续型特征，$\theta_1$、$\theta_2$、$\theta_3$分别是离散化后在使用one-hot或哑变量编码后的若干个特征表示。这时我们发现使用连续值的LR模型用一个权值去管理该特征，而one-hot后有三个权值管理了这个特征，这样使得参数管理的更加精细，所以这样拓展了LR模型的非线性能力。

　　这样做除了增强了模型的**非线性能力**外，还有什么好处呢？这样做了我们至少不用再去对变量进行归一化，也可以**加速**参数的更新速度；再者使得一个很大权值管理一个特征，拆分成了许多小的权值管理这个特征多个表示，这样做降低了特征值扰动对模型为**稳定性**影响，也降低了异常数据对模型的影响，进而使得模型具有更好的**鲁棒性**。