In this post, we describe linear machine learning models.

Let $U,V$ be finite dimensional real inner product spaces. The training data is a collection $D=\{(u_1,v_1),\dots,(u_r,v_r)\}$ of distinct pairs of vectors where $(u_i,v_i)\in U\times V$. 

Suppose that $A:U\rightarrow V$ is a linear transformation and $b\in V$. Then define the fitness function $F_D(A,b)$ by setting
$F_D(A,b)=\sum_{k=1}^{r}\log(\frac{\langle Au_k+b,v_k\rangle}{\|Au_k+b\|\cdot\|v_k\|}).$

