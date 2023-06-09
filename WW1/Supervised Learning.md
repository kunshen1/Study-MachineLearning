# 监督学习/Supervised Learning

**Reference Link**:https://zhuanlan.zhihu.com/p/56903924
---

## 概念
基本思想： 数据集中的每个样本都有相应的“正确答案”， 再依据这些样本做出预测。例如回归问题， 通过回归来推出一个连续的输出； 分类问题， 其目标是推出一组离散的结果。

## 模型
模型通常有两种分类方式：第一种是按模型形式分类：概率模型（Probabilistic Model）和 非概率模型（Non-probabilistic Model）；第二种是按是否对观测变量的分布建模分类：判别模型（Discriminative Model）和 生成模型（Generative Model）。这两种分类方法事实上把所有模型划分成了三类。
![image](./Picture/%E7%9B%91%E7%9D%A3%E5%AD%A6%E4%B9%A0%E6%A8%A1%E5%9E%8B.jpg)

模型一共分为图中的三种模型：非概率模型（Non-probabilistic Model）、概率判别模型（Probalilistic Discriminative Model）、生成模型（Generative Model）；三种模型挖掘信息的程度从少到多，解决问题的途径从直接到间接。其中，每种类别的代表性模型如下：

I. 非概率模型，直接判别：感知机（单层神经网络，Perceptron）、多层感知机（MLP）、支持向量机（SVM）、K近邻（KNN）

II. 概率判别模型，间接利用条件概率判别：逻辑回归（LR）、决策树（DT）、最大熵模型（ME）、条件随机场（CRF）

III. 生成模型，更间接地先求联合概率，然后利用贝叶斯定理判别：高斯判别分析（GDA）、朴素贝叶斯（NB）、受限玻尔兹曼机（RBM）、隐马尔科夫模型（HMM）


## 如何选择合适的监督学习算法
取决因素如下
1. 数据值的形式： 连续/离散
2. 数据维度： 大/小
3. 数据量： 多/少
4. 计算资源： CPU/GPU
5. 模型要求： 准确性， 效率
7. 模型可解释性： 虽然学习如何权衡输入变量的复杂组合能够带来更准确的预测，但它也使得机器学习模型变得更加困难，可悲解释的预测模型生成的决策，是由原始输入变量带来的，而不是输入变量的任意高阶组合，缩放，加权组合带来的，所以对特征进行操作越直观的模型可解释性越强。
![image](./Picture/%E7%9B%91%E7%9D%A3%E5%AD%A6%E4%B9%A0%E6%A8%A1%E5%9E%8B%E9%80%89%E6%8B%A9.webp)

我们可以根据数据值的因变量，或者称之为标签，是连续值还是离散值，将监督学习问题分为分类问题和回归问题，其中分类问题的标签是离散值，回归问题的标签是连续值.但是往后的节点需要根据 准确率和效率、可解释性、数据量 等指标对算法进行取舍。

![image](./Picture/%E6%97%B6%E9%97%B4%E5%A4%8D%E6%9D%82%E5%BA%A6.webp)
- **N**：训练样本 
- **M**: 样本特征维度 
- **P**：网络参数总个数 
- **D**：决策树层数
- **N<sub>sv</sub>**: 支持向量机

支持向量机，训练时间复杂度太高，这意味着样本数目太高训练效率很低；而且最后起作用的支持向量数目也是有限的，这意味着在特征维度一定的情况下，过多的训练样本数对模型预测准确率的提升也不大。所以综合两点，支持向量机适合小规模数据集。
K近邻，没有显式的训练过程，它的特点是完全跟着数据走，没有数学模型可言，也正因为如此具有很强的可解释性。表格中给的是 KD 树实现的时间复杂度，如果是朴素方法，训练时间复杂度更低一点，是 O(N M)，但预测时间复杂度高达 O(N logK)，效率极低。即使使用 KD 树实现，当特征维度稍微大一点，效率也是极低；所以K近邻法特征维度一般不超过20，实用价值严重受限。
神经网络，这里是以多层感知机（MLP）为例，现在深度学习层数和节点数目通常都比较大，所以网络参数个数P一般很大，P越大意味着越强的函数拟合能力，但前提是足够的计算资源和训练数据，所以说神经网络的表现效果一定程度上取决于计算资源和数据量。
逻辑回归，训练和预测效率都很高，多维输出时的Softmax层通常作为现在深度学习的最后一层，使用广泛，效果也良好。
决策树，决策树每个节点有十分具体的物理意义，所以有很强的解释性，训练效率较快，当我们希望能更好地理解手头数据的时候，往往可以使用决策树。但也是受限于其简单性，决策树更大的用处是作为一些更有用的算法的基石，比如随机森林，还有 BAT、华为等公司大数据比赛 几年前流行的算法 GBDT，和最近几年流行的算法 XGBoost。
朴素贝叶斯，跟K近邻类似，也没有显式的训练过程，因此也有较强的可解释性，这一点与图X结论不太一样哈。训练和预测效率效率都很高。典型的应用场景就是垃圾邮件过滤器，效果一般会很好。
高斯判别模型，高斯判别模型是基于伯努利分布的，这一点与逻辑回归一致，事实上高斯判别模型求得的后验概率跟逻辑回归的函数形式也是一致的，差别就在于高斯判别模型多一个对各个类别数据本身的分布假设——高斯分布，这意味着高斯判别模型比逻辑回归需要更加严格的模型假设，在实践中，逻辑回归比高斯判别模型的泛化性能更强。除此之外，计算过程需要求 “特征X” 减 “特征期望” 的协方差矩阵，所以效率会比逻辑回归低一点。
总的来说，就像机器学习领域中惯用的一句话，没有最好的模型，只有最合适的模型，这句话很zhengzhi正确。但我认为，就实际应用的准确率来看，深度神经网络 > 支持向量机 > 其它，另外有一些像英语老师常说的 “固定搭配、死记住” 的一些适合特殊场景的算法，比如 垃圾邮件过滤器——朴素贝叶斯模型，类别性质的稀疏特征——逻辑回归模型，大数据推荐算法——XGBoost 等经验性质结论，不一定完美，但效果一定不错。

