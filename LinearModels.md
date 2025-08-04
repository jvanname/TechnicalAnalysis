In this post, we describe linear machine learning models.

Let $U,V$ be finite dimensional real inner product spaces. The training data is a collection $D=\{(u_1,v_1),\dots,(u_r,v_r)\}$ of distinct pairs of vectors where $(u_i,v_i)\in U\times V$. 

Suppose that $A:U\rightarrow V$ is a linear transformation and $b\in V$. Then define the fitness function $F_D(A,b)$ by setting
$F_D(A,b)=\sum_{k=1}^{r}\log(\frac{\langle Au_k+b,v_k\rangle}{\|Au_k+b\|\cdot\|v_k\|}).$

Observe that $F_D$ is a partial function because we cannot take a logarithm of a negative real number. 



Suppose that $(e_1,\dots,e_n)$ is an orthonormal basis of $V$ and $v_i\in\{e_1,\dots,e_n\}$ for all $n$. Suppose that $F_D(A,b)$ is locally maximized. Let $j\in\{1,\dots,r\}$. Set $w=\frac{Au_j+b}{\|Au_j+b\|}$. Then
$\langle w,e_1\rangle^2+\dots+\langle w,e_n\rangle^2=1$. Here, the value $\langle w,e_k\rangle^2$ is the probability of returning the state $e_k$ when measuring the quantum state $w$ with respect to the basis
$\{e_1,\dots,e_n\}$. In terms of our machine learning model, the value $\langle w,e_k\rangle^2$ may be interpreted as the probability of returning the state
