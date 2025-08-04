In this post, we describe linear machine learning models.

Let $U,V$ be finite dimensional real inner product spaces. The training data is a collection $D=\{(u_1,v_1),\dots,(u_r,v_r)\}$ of distinct pairs of vectors where $(u_i,v_i)\in U\times V$. 

Suppose that $A:U\rightarrow V$ is a linear transformation and $b\in V$. Then define the fitness function $F_D(A,b)$ by setting
$F_D(A,b)=\sum_{k=1}^{r}\log(\frac{\langle Au_k+b,v_k\rangle}{\|Au_k+b\|\cdot\|v_k\|})/r.$

Observe that $F_D$ is a partial function because we cannot take a logarithm of a negative real number. 

Suppose that $(e_1,\dots,e_n)$ is an orthonormal basis of $V$ and $v_i\in\{e_1,\dots,e_n\}$ for all $n$. Suppose that $F_D(A,b)$ is locally maximized. Let $j\in\{1,\dots,r\}$. Set $w=\frac{Au_j+b}{\|Au_j+b\|}$. Then
$\langle w,e_1\rangle^2+\dots+\langle w,e_n\rangle^2=1$. Here, the value $\langle w,e_k\rangle^2$ is the probability of returning the state $e_k$ when measuring the quantum state $w$ with respect to the basis
$\{e_1,\dots,e_n\}$. In terms of our machine learning model, the value $\langle w,e_k\rangle^2$ may be interpreted as the probability that $e_k=v_j$ and the following proposition justifies this interpretation of $\langle w,e_k\rangle^2$.

Proposition: Suppose that $e_1,\dots,e_n$ is an orthonormal basis of a real inner product space $V$. Let $(p_1,\dots,p_n)$ be a probability vector with $p_j>0$ for all $j.$ Then there is a unique vector $x$ where
$\|x\|=1$, $\langle x,e_j\rangle>0$ and where the quantity $L(x)=\sum_{k=1}^{n}p_k\cdot\log(\frac{\langle x,e_k\rangle}{\|x\|})$ is locally maximized, namely $x=\sum_{k=1}^{p}\sqrt{p_k}\cdot e_k$.

Proof: Suppose that $x=x_1 e_1+\dots+x_r e_r$. Then $\langle x,e_k\rangle=x_k$ and $L(x)=\sum_{k=1}^{n}p_k\cdot\log(\frac{x_k}{\sqrt{x_1^2+\dots+x_n^2}}=(\sum_{k=1}^{n}p_k\cdot\log(x_k))-\log(x_1^2+\dots+x_n^2)/2$.

Then $\frac{\partial}{\partial x_\alpha}L(x)=\frac{p_\alpha}{x_\alpha}-\frac{x_\alpha}{x_1^2+\dots+x_n^2}$. If $L(x)$ is locally maximized, then for each $\alpha$, we have
$0=\frac{\partial}{\partial x_\alpha}L(x)$ for all $\alpha$ which implies that $\frac{x_\alpha}{x_1^2+\dots+x_n^2}=\frac{p_\alpha}{x_\alpha}$. Since $\|x\|=1$, we have
$x_\alpha=\frac{p_\alpha}{x_\alpha}$, so $x_\alpha^2=p_\alpha$, hence $x_\alpha=\sqrt{p_\alpha}$.





