[TOC]
# 向量投影和最小二乘法

## 1. 向量的投影

- 问题1: 某个向量$b=(2,3,4)$投影到z轴或者xy平面, 投影的结果长什么样子?  
- 问题2: 什么样的矩阵能够把向量$b$投影到一条线或者一个平面?   

定义: $b$在线上的投影属于该条线, $b$在平面上的投影属于该平面. 投影结果$p=Pb$. 其中$P$为投影矩阵.  
投影问题的定义: $b$向$A$的列空间进行投影. $A$是mxn的矩阵.  

### 1.1 向量在向量上的投影

![Fig1](/home/fqy/project/blog/support_files/Fig1.png)
error $e = b - \widehat{x}a$, $\widehat{x}$是某个系数, 使得$b$在$a$上的投影$p = \widehat{x}a$.    
根据投影中的关键性质: 正交性质. 可得$a$和误差$e$正交, 即:  
$a \cdot p = 0$ $\Leftrightarrow$  $a \cdot (b - \widehat{x}a) = 0 $, 推出 $\widehat{x} = \frac{a \cdot b}{a \cdot a} = \frac{a^T b}{a^T a}$  
$\therefore$ 投影$p = \widehat{x}a = a \widehat{x} = a\frac{a^T b}{a^T a} = \frac{a \cdot a^T}{a^T a}b = Pb$  
定义投影矩阵$P = \frac{a \cdot a^T}{a^T a}$.  

### 1.2 向量在空间上的投影

![Fig2](/home/fqy/project/blog/support_files/Fig2.png)
定义空间S由n个线性无关的向量张成. $A = [a_1, a_2, ... , a_n], a_1, a_2, ... , a_n \subset \mathbb{R}^m$  
向量$b \subset \mathbb{R}^m$ 在A的列空间上的投影结果记为:  
$$
p = \widehat{x_1}a_1 + \widehat{x_2}a_2 + ... + \widehat{x_n}a_n = A \widehat{x}
$$
同理, 根据投影的正交性质, 被投影的空间$A$和误差$e = b - p$是正交的. 即误差向量$e$和$A$的列空间中的每一个列向量都正交, 二者之间的内积为0, 因此有如下关系:  
$$
\begin{matrix}
\\ a_1^T(b - A \widehat{x}) = 0
\\ a_2^T(b - A \widehat{x}) = 0
\\ ...
\\ a_n^T(b - A \widehat{x}) = 0
\end{matrix}
$$
等价于:  
$$
A^T(b - A \widehat{x}) = 0 \Leftrightarrow A^TA\widehat{x} = A^Tb 
$$ 右边的这个方程称之为法线方程.  
注意:  
$A^TA$是一个对称矩阵,大小为nxn, 因为A的所有n个列向量是线性无关的, 所以$A^TA$是可逆的.  
$\therefore$ 可以求解得到投影结果$p = A\widehat{x} = A(A^TA)^{-1}A^Tb = Pb$  
定义投影矩阵$P = A (A^TA)^{-1}A^T$.  

如此可以看出, 当被投影的空间退化成一个列向量时, 即得到了1.1中的向量投影到向量的结论.  

## 2. 最小二乘法

###  2.1 最小二乘法近似

### 2.2 直线和抛物线的拟合


## 3. 参考资料

[[1] Strang G, Strang G, Strang G, et al. Introduction to linear algebra[M]. Wellesley, MA: Wellesley-Cambridge Press, 1993.](http://math.mit.edu/~gs/linearalgebra/)