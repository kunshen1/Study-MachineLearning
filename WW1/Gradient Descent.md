# Gradient Descent

**Reference Link**: https://mp.weixin.qq.com/s?__biz=MzIwOTc2MTUyMg==&mid=2247507430&idx=2&sn=5d1deb023b009c32cce3d37e37f2efac&chksm=976c787ba01bf16d15432a341cb0733e8012ebf5dc23d7914944d1c1e2731e7a2e4d9a1fb365&scene=21#wechat_redirect

---

## 概述

梯度下降是一个用来求函数最小值的算法。
方法思路： 开始随机选取一个参数的组合 $\left( {\theta_{0}},{\theta_{1}},......,{\theta_{n}} \right)$, 计算代价函数， 然后寻找下一个能让代价函数值下降最多的参数组合， 直到找到一个局部最小值。 因为没有尝试完所有的参数组合，所以无法确认得到的局部最小值是否是全局最小值，选择不同的参数组合可能回得到不同的局部最小值。
![](./Picture/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D.jpg)

批量梯度下降算法(Batch gradient descent)公式：

![](./Picture/%E6%89%B9%E9%87%8F%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E5%85%AC%E5%BC%8F.png)

其中$\alpha$是学习率(learning rate), 它决定了我们沿着代价函数下降程度最大方向向下卖出的步子有多大，在批量梯度下降中，我们每一次都同时让所有的参数减去学习速率乘以代价函数的导数。

![](./Picture/%E6%89%B9%E9%87%8F%E4%BB%A3%E4%BB%B7%E5%87%BD%E6%95%B0%E8%AE%A1%E7%AE%97.png)

在梯度下降算法中，还有一个更微妙的问题，梯度下降中，我们要更新${\theta_{0}}$和${\theta_{1}}$ ，当 $j=0$ 和$j=1$时，会产生更新，所以你将更新$J\left( {\theta_{0}} \right)$和$J\left( {\theta_{1}} \right)$。实现梯度下降算法的微妙之处是，在这个表达式中，如果你要更新这个等式，你需要同时更新${\theta_{0}}$和${\theta_{1}}$，我的意思是在这个等式中，我们要这样更新：

${\theta_{0}}$:= ${\theta_{0}}$ ，并更新${\theta_{1}}$:= ${\theta_{1}}$。

实现方法是：你应该计算公式右边的部分，通过那一部分计算出${\theta_{0}}$和${\theta_{1}}$的值，然后同时更新${\theta_{0}}$和${\theta_{1}}$。

![](./Picture/%E5%90%8C%E6%97%B6%E8%B7%9F%E6%96%B0.png)

$\alpha \frac{\partial }{\partial {{\theta }_{0}}}J({{\theta }_{0}},{{\theta }_{1}})$，$\alpha \frac{\partial }{\partial {{\theta }_{1}}}J({{\theta }_{0}},{{\theta }_{1}})$

## 梯度下降直观理解
梯度下降算法：${\theta_{j}}:={\theta_{j}}-\alpha \frac{\partial }{\partial {\theta_{j}}}J\left(\theta \right)$

![](./Picture/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E7%9B%B4%E8%A7%82%E7%90%86%E8%A7%A3.png)

学习率：α是学习率它决定了我们沿着能让代价函数下降程度最大的方向向下迈出的步子有多大。

学习率太小：收敛速度慢需要很长的时间才会到达全局最低点

学习率太大：可能越过最低点，甚至可能无法收敛

![](./Picture/%E5%9B%BA%E5%AE%9A%E5%AD%A6%E4%B9%A0%E7%8E%87.jfif)

## 梯度下降的线性回归

梯度下降是很常用的算法，它不仅被用在线性回归上和线性回归模型、平方误差代价函数。将梯度下降和代价函数相结合。

![](./Picture/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E7%BA%BF%E6%80%A7%E5%9B%9E%E5%BD%92.jfif)

**批量梯度下降算法**对之前的线性回归问题运用梯度下降法，关键在于求出代价函数的导数，

![](./Picture/%E6%89%B9%E9%87%8F%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E7%AE%97%E6%B3%95.jfif)


这种梯度下降的算法称之为批量梯度下降算法，主要特点：

- 在梯度下降的每一步中，我们都用到了所有的训练样本

- 在梯度下降中，在计算微分求导项时，我们需要进行求和运算,需要对所有m个训练样本求和



