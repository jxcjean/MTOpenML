# 机器学习-72:机器学习的回归算法实战(含sklearn源码)

> [机器学习原理与实践(开源图书)-总目录](https://blog.csdn.net/shareviews/article/details/83030331)

诸事有因，回归(Regression)算法通过建立变量之间的回归模型，通过学习(训练)过程得到变量与因变量之间的相关关系。回归(Regression)分析可以用于预测模型或分类模型。常见的回归算法包括：线性回归(Linear Regression)、非线性回归(Non-linear Regression)、逻辑回归(Logistic Regression)、多项式回归(Polynomial Regression)、岭回归(Ridge Regression)、套索回归(Lasso Regression)和弹性网络回归(ElasticNet Regression)。其中线性回归、非线性回归和逻辑回归最为常用。

> 告别碎片阅读，构成知识谱系。一起阅读和完善: [机器学习原理与实践(开源图书)](https://github.com/media-tm/MTOpenML)

## 算法概述

本代码构建线性函数和多项式函数并绘图。然后在用SkLearn的线性回归(LinearRegression)模块和多项式回归(PolynomialFeatures)模块拟合上述两种曲线。

完整源码见: code-ml/code-sklearn/ml-sklearn-regression.py

## 构建线性函数和多项式函数

构造线性函数： $h(x)=0.3-0.05*x$,并在线性函数上添加随机值；构造多项式函数 $h(x)=0.1-0.02*x+0.03*x^2-0.04*x^3$，并在多项式函数上添加随机值；

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

sample_cnt= 32

data_x = np.linspace(start = 0, stop = sample_cnt/4, num = sample_cnt).reshape(-1, 1)
rand_n = np.random.randn(sample_cnt).reshape(-1, 1)

# curve using linear
curve_linear = np.sin(data_x)
θ0, θ1 = 0.3, -0.05
curve_linear = yr = θ0 + θ1*data_x
curve_linear += rand_n * 0.03

# curve using polynomial
θ0, θ1, θ2, θ3 = 0.1, -0.02, 0.03, -0.04
curve_polynomial = θ0 + θ1*data_x + θ2*(data_x**2) + θ3*(data_x**3)
curve_polynomial += rand_n

plt.subplot(2, 2, 1)
plt.plot(data_x, curve_linear, 'b.')
plt.xlabel("np.linspace(0, 8, 32)")
plt.ylabel("curve_linear(data_x)")

plt.subplot(2, 2, 2)
plt.plot(data_x, curve_polynomial, 'b.')
plt.xlabel("np.linspace(0, 8, 32)")
plt.ylabel("curve_polynomial(data_x)")
```

## SkLearn线性回归

使用SkLearn的LinearRegression模块拟合曲线。可以使用sklearn.metrics.mean_squared_error 评估误差。从结果可见，使用线性函数去拟合多项式函数效果很差。

- 对于线性数据集，线性拟合函数的MSE为0.00069
- 多余多项式数据集，线性拟合函数的MSE为6.40752

```python
    linear_reg = LinearRegression()
    linear_reg.fit(data_x, curve_linear)
    print(linear_reg.intercept_, linear_reg.coef_)
    fit_x = np.linspace(start = 0, stop = sample_cnt/4, num = 1024).reshape(-1, 1)
    fit_linear = np.dot(fit_x, linear_reg.coef_.T) + linear_reg.intercept_

    plt.subplot(2, 2, 3)
    plt.plot(fit_x, fit_linear, 'r-')
    plt.plot(data_x, curve_linear, 'b.')
    plt.xlabel("np.linspace(0, 8, 32)")
    plt.ylabel("curve fitting using Linear")

    linear_reg_fail = LinearRegression()
    linear_reg_fail.fit(data_x, curve_polynomial)
    print(linear_reg_fail.intercept_, linear_reg_fail.coef_) 
    fit_x = np.linspace(start = 0, stop = sample_cnt/4, num = 1024).reshape(-1, 1)
    fit_linear_fail = np.dot(fit_x, linear_reg_fail.coef_.T) + linear_reg_fail.intercept_

    plt.subplot(2, 2, 4)
    plt.plot(fit_x, fit_linear_fail, 'r-')
    plt.plot(data_x, curve_polynomial, 'b.')
    plt.xlabel("np.linspace(0, 8, 32)")
    plt.ylabel("curve fitting using Linear")

    hypo = np.dot(data_x, linear_reg.coef_.T) + linear_reg.intercept_
    hypo_fail = np.dot(data_x, linear_reg_fail.coef_.T) + linear_reg_fail.intercept_
    print(mean_squared_error(hypo, curve_linear))          # MSE: 0.00069
    print(mean_squared_error(hypo_fail, curve_polynomial)) # MSE: 6.40752
```

## SkLearn多项式回归

使用SkLearn的LinearRegression模块拟合曲线。可以使用sklearn.metrics.mean_squared_error 评估误差。从结果可见，多项式函数可以拟合线性函数，但是出现过拟合现象。多项式函数拟合多项式函数最佳，但是也需要多项式的阶数，用高阶多项式函数拟合低阶多项式函数也会出现过拟合现象。

- 对于线性数据集，多项式拟合函数的MSE为0.00055
- 多余多项式数据集，多项式拟合函数的MSE为0.61483

```python
    poly_features_1 = PolynomialFeatures(degree = 3)
    linear_reg = LinearRegression()
    linear_reg.fit(poly_features_1.fit_transform(data_x), curve_linear)
    print(poly_features_1.get_params())
    fit_x = np.linspace(start = 0, stop = sample_cnt/4, num = 1024).reshape(-1, 1)
    fit_linear = linear_reg.predict(poly_features_1.fit_transform(fit_x))

    plt.subplot(2, 2, 3)
    plt.plot(fit_x, fit_linear, 'r-')
    plt.plot(data_x, curve_linear, 'b.')
    plt.xlabel("np.linspace(0, 8, 32)")
    plt.ylabel("curve fitting using Polynomial")

    poly_features_3 = PolynomialFeatures(degree = 3)
    linear_reg_best = LinearRegression()
    linear_reg_best.fit(poly_features_3.fit_transform(data_x), curve_polynomial)
    fit_x = np.linspace(start = 0, stop = sample_cnt/4, num = 1024).reshape(-1, 1)
    fit_linear_best = linear_reg_best.predict(poly_features_3.fit_transform(fit_x))

    plt.subplot(2, 2, 4)
    plt.plot(fit_x, fit_linear_best, 'r-')
    plt.plot(data_x, curve_polynomial, 'b.')
    plt.xlabel("np.linspace(0, 8, 32)")
    plt.ylabel("curve fitting using Polynomial")

    hypo = linear_reg.predict(poly_features_1.fit_transform(data_x))
    hypo_best = linear_reg_best.predict(poly_features_3.fit_transform(data_x))
    print(mean_squared_error(hypo, curve_linear))          # MSE: 0.00055
    print(mean_squared_error(hypo_best, curve_polynomial)) # MSE: 0.61483
```

## 系列文章

- [深度学习原理与实践(开源图书)-总目录](https://blog.csdn.net/shareviews/article/details/83040730)
- [机器学习原理与实践(开源图书)-总目录](https://blog.csdn.net/shareviews/article/details/83030331)
- [Github: 机器学习&深度学习理论与实践(开源图书)](https://github.com/media-tm/MTOpenML)

## 参考资料

- [1] 周志华. 机器学习. 清华大学出版社. 2016.
- [2] [日]杉山将. 图解机器学习. 人民邮电出版社. 2015.
- [3] 佩德罗·多明戈斯. 终极算法-机器学习和人工智能如何重塑世界. 中信出版社. 2018.
- [4] [sklearn.preproccessing库官方文档]