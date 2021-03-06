# 机器学习-11:机器学习的分类

> [机器学习原理与实践(开源图书)-总目录](https://blog.csdn.net/shareviews/article/details/83030331)

根据不同的概念和意图可以将机器学习算法分成若干类别。本文主要按照学习形式分类、任务目标分类和学习策略的不同分类。我们试图对机器学习算法进行分类，分类的目的在于找到机器学习算法的共性、个性和适用边界。方便我们针对特定的问题域快速评估出可行的解决方案。

> 告别碎片阅读，构成知识谱系。一起阅读和完善: [机器学习原理与实践(开源图书)](https://github.com/media-tm/MTOpenML)

## 1 学习形式分类

按照学习形式的不同可以将机器学习算法分为监督学习、非监督学习和强化学习算法。

### 1.1 监督学习(Supervised Learning)

在监督学习中，要求用于训练算法的训练集必须包含明确的标识或结果。在建立预测模型的时候，监督式学习建立一个学习过程，将预测结果与“训练数据”的实际结果进行比较，不断的调整预测模型，直到模型的预测结果达到一个预期的准确率。监督式学习的常见应用场景如分类问题和回归问题。常见算法有逻辑回归(Logistic Regression)和BP神经网络(Back Propagation Neural Network)。

### 1.2 非监督学习(Unsupervised Learning) 

在非监督式学习中，数据并不被特别标识，学习模型是为了推断出数据的一些内在结构。常见的应用场景包括关联规则的学习以及聚类等。常见算法包括Apriori算法以及k-Means算法。

### 1.3 强化学习(Reinforcement Learning)

在强化学习中，输入数据直接反馈到模型，模型必须对此立刻作出调整。常见的应用场景包括动态系统以及机器人控制等。常见算法包括Q-Learning以及时间差学习(Temporal difference learning)。在自动驾驶、视频质量评估、机器人等领域强化学习算法非常流行。

## 2 任务目标分类

按照任务目标的不同可以将机器学习算法分为回归算法、分类算法和聚类算法。

### 2.1 回归算法

诸事有因，回归(Regression)算法通过建立变量之间的回归模型，通过学习(训练)过程得到变量与因变量之间的相关关系。回归(Regression)分析可以用于预测模型或分类模型。常见的回归算法包括：线性回归(Linear Regression)、非线性回归(Non-linear Regression)、逻辑回归(Logistic Regression)、多项式回归(Polynomial Regression)、岭回归(Ridge Regression)、套索回归(Lasso Regression)和弹性网络回归(ElasticNet Regression)。其中线性回归、非线性回归和逻辑回归最为常用。

### 2.2 分类算法

机器学习分为监督学习、无监督学习和半监督学习(强化学习)。无监督学习最常应用的场景是聚类(clustering)和降维(dimension reduction)。分类算法和回归算法都属于监督学习算法, 其中分类算法的目标就是：学习数据集的数据特征，并将原始数据特征映射到目标的分类类别。分类算法包括：逻辑回归(Logistic Regression, LR)、K最近邻(k-Nearest Neighbor, KNN)、朴素贝叶斯模型(Naive Bayesian Model, NBM)、隐马尔科夫模型(Hidden Markov Model)、支持向量机(Support Vector Machine)、决策树(Decision Tree)、神经网络(Neural Network)和集成学习(ada-boost)。其中集成学习(ada-boost)是一个混合分类方法。

### 2.3 聚类算法

机器学习分为监督学习、无监督学习和半监督学习(强化学习)。无监督学习从无标签的数据集中挖掘和发现数据的数理规律。有监督学习从有标签的数据集中挖掘和发现的数据的数理规律。最终机器学习从数据集中得到的模型具有相当的泛化能力，能够处理新的数据输入，并作出合理的预测。有监督学习和无监督学习的最大区别在于数据是否有标签。无监督学习最常应用的场景是聚类(clustering)和降维(dimension reduction)。

聚类算法包括：K均值聚类(K-Means)、层次聚类(Hierarchical Clustering)和混合高斯模型(Gaussian Mixture Model)。降维算法包括：主成因分析(Principal Component Analysis)和线性判别分析(Linear Discriminant Analysis)。

## 3 学习策略分类

按照学习策略的不同可以将机器学习算法分为演绎学习、演绎学习和类比学习等。

### 3.1 演绎学习 (Learning by deduction)

学生所用的推理形式为演绎推理。推理从公理出发，经过逻辑变换推导出结论。这种推理是"保真"变换和特化(specialization)的过程，使学生在推理过程中可以获取有用的知识。这种学习方法包含宏操作(macro-operation)学习、知识编辑和组块(Chunking)技术。演绎推理的逆过程是归纳推理。

### 3.2 演绎学习 (Learning from induction)

归纳学习是由教师或环境提供某概念的一些实例或反例，让学生通过归纳推理得出该概念的一般描述。这种学习的推理工作量远多于示教学习和演绎学习，因为环境并不提供一般性概念描述（如公理）。从某种程度上说，归纳学习的推理量也比类比学习大，因为没有一个类似的概念可以作为"源概念"加以取用。归纳学习是最基本的，发展也较为成熟的学习方法，在人工智能领域中已经得到广泛的研究和应用。

### 3.3 类比学习 (Learning by analogy)

利用二个不同领域（源域、目标域）中的知识相似性，可以通过类比，从源域的知识（包括相似的特征和其它性质）推导出目标域的相应知识，从而实现学习。类比学习系统可以使一个已有的计算机应用系统转变为适应于新的领域，来完成原先没有设计的相类似的功能。

## 系列文章

- [深度学习原理与实践(开源图书)-总目录](https://blog.csdn.net/shareviews/article/details/83040730)
- [机器学习原理与实践(开源图书)-总目录](https://blog.csdn.net/shareviews/article/details/83030331)
- [Github: 机器学习&深度学习理论与实践(开源图书)](https://github.com/media-tm/MTOpenML)

## 参考文献

- [1] 周志华. 机器学习. 清华大学出版社. 2016.
- [2] [日]杉山将. 图解机器学习. 人民邮电出版社. 2015.
- [3] 佩德罗·多明戈斯. 终极算法-机器学习和人工智能如何重塑世界. 中信出版社. 2018.
