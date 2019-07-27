[TOC]

# 正交基和Gram-Schmidt正交化

## 1. 正交基的一些概念

本文的两个目的:  
- 在求最小二乘解$\widehat{x}$, 投影$p$, 投影矩阵$P$的时候, 使用正交性质会使问题变简单. 因为在$A$的列向量正交的性质下, 正交方程中的$A^TA$变成了对角阵.  
- 如何将原向量组变成正交的向量组, 二者之间的变换关系如何描述.  

正交向量组定义如下:  
![在这里插入图片描述](https://img-blog.csdnimg.cn/201907251846332.png)

正交矩阵的定义: 如果向量组构成的矩阵为方阵, 称为正交矩阵, 有如下的另外性质:  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725184823515.png)

正交矩阵的性质:  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725191644785.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plZmZZb3VuZ19yZWdpc3RlcmVk,size_16,color_FFFFFF,t_70)

关于正交矩阵的一个例子: 旋转矩阵:  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725185217458.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725185225818.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plZmZZb3VuZ19yZWdpc3RlcmVk,size_16,color_FFFFFF,t_70)

## 2. 通过正交投影进行矩阵的正交化
如果$Ax = b$求最小二乘解, 可知:  
$$
A^TA \widehat{x} = A^Tb
$$
如果矩阵A(不一定是方阵)中的所有列向量正交. 那么: $Qx = b$求最小二乘解有: 
$$
Q^TQ\widehat{x} = Q^Tb \Rightarrow \widehat{x} = Q^Tb  
$$
投影矩阵$P$:  
$$
P = Q(Q^TQ)^-1Q^T \Rightarrow P = QQ^T
$$

**为什么要去搞什么正交化呢?**  
因为正交的向量组有性质$Q^TQ = I$, 而在求解最小二乘解的时候会出现$A^TA$这种结构, 所以如果求解的方程组$Ax = b$中的矩阵$A$是一个正交矩阵, 那么求解会变得简单许多.  

**Gram-schmidt正交化**
- 输入: 矩阵$A = \begin{bmatrix} a&b&c \end{bmatrix}$, 向量之间线性无关.  
- 输出: 向量之间正交的矩阵$X = \begin{bmatrix} x&y&z \end{bmatrix}$, 对向量进行归一化后的矩阵$Q = \begin{bmatrix} q_1&q_2&q_3 \end{bmatrix}$, $q_1 = \frac{x}{\left \|x\right \|}$, 以此类推.  

(1) 先选择第一个向量, 不妨就另$x = a$.  
(2) 第二个正交向量, 根据正交投影思想, $b$投影到$x$的分量为$p_b$, $b - p_b = e_b = y$, 误差向量$e_b = y$, $y$垂直与$x$, $y = b -  \frac{x^Tb}{x^Tx}x$ .  
(3) 第三个向量, 同理, $c$投影到$x$和$y$构成的子空间上为投影向量$p_c$, $c - p_c = e_c = z$, 误差向量$e_c = z$垂直于$x$ 和$y$, $z = c -  \frac{x^Tc}{x^Tx}x -  \frac{y^Tc}{y^Ty}y$ .  
从上面可以发现: 这种正交化的方法是有次序的, 比如得到的$q_2$只和向量$a, b$有关系, 和$c$没有关系.  

## 3. QR分解

上面提到的正交化前后的矩阵:  
- 输入: 矩阵$A = \begin{bmatrix} a&b&c \end{bmatrix}$, **向量之间线性无关**.  
- 输出: 矩阵$Q = \begin{bmatrix} q_1&q_2&q_3 \end{bmatrix}$, $q_1 = \frac{x}{\left \|x\right \|}$, 以此类推.  
那么二者之间是什么关系呢???  
$$
\begin{bmatrix} &q_1&\\&q_2&\\&q_3& \end{bmatrix}
\begin{bmatrix} \\a&b&c\\ \\ \end{bmatrix}
= \begin{bmatrix} q_1^{T}a & q_1^{T}b & q_1^{T}c \\ & q_2^{T}b & q_2^{T}c \\ & & q_3^{T}c \end{bmatrix}
$$
定义其中的上三角矩阵为R, 有:  
$$
Q^TA = R \Rightarrow A = QR
$$
**注意**: 假设矩阵A为mxn, 那么这个上三角矩阵$R$为nxn, 并且**对象线上的元素都大于0**, 所以矩阵$R$可逆.  

- 回顾最小二乘的求解方程:  

$$A^TA\widehat{x} = A^Tb$$
对矩阵A进行QR分解后,有:  
$$
A^TA = R^TQ^TQR = R^TR
\Rightarrow R^TR\widehat{x} = R^TQ^Tb
\Rightarrow R\widehat{x} = Q^Tb
\Rightarrow \widehat{x} = R^{-1}Q^Tb
$$
从上面可以看出来: 对于这个式子, $R\widehat{x} = Q^Tb$, 因为R为上三角矩阵, 所以可以用回代法一步步倒解$\widehat{x}$ .  

## 4. 参考

[[1] Strang G, Strang G, Strang G, et al. Introduction to linear algebra[M]. Wellesley, MA: Wellesley-Cambridge Press, 1993.](http://math.mit.edu/~gs/linearalgebra/)

## 总结
对于矩阵$A$, 大小为mxn, 不要求为方阵.  如果A中的列向量线性无关, 那么可以进行QR分解. 目的是为了方便求解$Ax=b$这样的最小二乘解.  
