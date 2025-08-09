In this post, we describe linear machine learning models.

Let $U,V$ be finite dimensional real inner product spaces. The training data is a collection $D=\{(u_1,v_1),\dots,(u_r,v_r)\}$ of distinct pairs of vectors where $(u_i,v_i)\in U\times V$. 

Suppose that $A:U\rightarrow V$ is a linear transformation and $b\in V$. Then define the fitness function $F_D(A,b)$ by setting
$F_D(A,b)=\sum_{k=1}^{r}\log(\frac{\langle Au_k+b,v_k\rangle}{\|Au_k+b\|\cdot\|v_k\|})/r.$

Observe that $F_D$ is a partial function because we cannot take a logarithm of a negative real number. Fortunately, $F_D$ is approximately $-\infty$ near the boundary of $F_D$, so gradient ascent training will not move the input of $F_D$ outside the domain of
$F_D$ unless the learning rate is too high.

Suppose that $(e_1,\dots,e_n)$ is an orthonormal basis of $V$ and $v_i\in\{e_1,\dots,e_n\}$ for all $n$. Suppose that $F_D(A,b)$ is locally maximized. Let $j\in\{1,\dots,r\}$. Set $w=\frac{Au_j+b}{\|Au_j+b\|}$. Then
$\langle w,e_1\rangle^2+\dots+\langle w,e_n\rangle^2=1$. Here, the value $\langle w,e_k\rangle^2$ is the probability of returning the state $e_k$ when measuring the quantum state $w$ with respect to the basis
$\{e_1,\dots,e_n\}$. In terms of our machine learning model, the value $\langle w,e_k\rangle^2$ may be interpreted as the probability that $e_k=v_j$ and the following proposition justifies this interpretation of $\langle w,e_k\rangle^2$. We shall call the value
$\langle w,e_k\rangle$ an amplitude.

Proposition: Suppose that $e_1,\dots,e_n$ is an orthonormal basis of a real inner product space $V$. Let $(p_1,\dots,p_n)$ be a probability vector with $p_j>0$ for all $j.$ Then there is a unique vector $x$ where
$\|x\|=1$, $\langle x,e_j\rangle>0$ and where the quantity $L(x)=\sum_{k=1}^{n}p_k\cdot\log(\frac{\langle x,e_k\rangle}{\|x\|})$ is locally maximized, namely $x=\sum_{k=1}^{p}\sqrt{p_k}\cdot e_k$. In other words,
$\langle x,e_k\rangle^2=p_k$ for all $k$.

Proof: Suppose that $x=x_1 e_1+\dots+x_r e_r$. Then $\langle x,e_k\rangle=x_k$ and $L(x)=\sum_{k=1}^{n}p_k\cdot\log(\frac{x_k}{\sqrt{x_1^2+\dots+x_n^2}}=(\sum_{k=1}^{n}p_k\cdot\log(x_k))-\log(x_1^2+\dots+x_n^2)/2$.

Then $\frac{\partial}{\partial x_\alpha}L(x)=\frac{p_\alpha}{x_\alpha}-\frac{x_\alpha}{x_1^2+\dots+x_n^2}$. If $L(x)$ is locally maximized, then for each $\alpha$, we have
$0=\frac{\partial}{\partial x_\alpha}L(x)$ for all $\alpha$ which implies that $\frac{x_\alpha}{x_1^2+\dots+x_n^2}=\frac{p_\alpha}{x_\alpha}$. Since $\|x\|=1$, we have
$x_\alpha=\frac{p_\alpha}{x_\alpha}$, so $x_\alpha^2=p_\alpha$, hence $x_\alpha=\sqrt{p_\alpha}$. Q.E.D.

**Example 0: Discrete probability distribution** 

**Example 1: Continuous probability distribution** Let $S_1=\{(\alpha,\beta):\alpha^2+\beta^2=1\}$ which is the unit circle. Suppose that our training data is a collection
$(u_k,w_k)$ where $u_k\in U$ and $w_k\in S_1$ for all $k$. When working with real world data, one may need to process the training data so that it is of this form.
If $(a,b)\in\mathbb{R}^2$, then define $(a,b)^{\otimes n}=(\sqrt{\binom{n}{k}}a^{n-k}b^k)_{k=0}^n$. Define $v_k=w_k^{\otimes n}$ for all $k$. Just as our linear model gives us a probability mass function for a discrete distribution for each input, in this
case, our linear model gives s probability density function for each input.

Suppose that $(A,b)$ is our trained model. Let $w=(A u_k+b)/\|A u_k+b\|$. Then let $f:S_1\rightarrow\mathbb{R}$ be the function defined by setting
$f(a,b)=\langle w,(a,b)^{\otimes n}\rangle$. Let $g=f/\|f\|_2$ where $\|*\|_2$ denotes the $L_2$-norm with respect to the Haar probability measure on $S_1$ and let $h=g^2$. Then $h$ is a probability density function on the circle $S_1$ that represents the distribution of possibe values of $w_k$.

**Initialization** The pair $A,b$ is initialized so that $\langle Au_k+b,v_k\rangle>0$ for all $k$. This is usually easy to do if it is possible, but on rare occasions, we will need to use more machine learning to find an input
$A,b$ where $\langle Au_k+b,v_k\rangle>0$ for all $k$. It is sufficient to initialize $A=\mathbf{0}$ and where $\langle b,v_k\rangle>0$ for all $k$.

**Pseudodeterminism:** If we find a local maximum of $F_D$ using gradient ascent multiple times, we will tend to produce the exact same local maximum.

**Advantages:** The models obtained by maximizing $F_D$ are simple, interpretable, mathematical, and they produce actual probabilities that can be interpreted in terms of quantum states.

**Disadvantages:** Models trained to maximize $F_D$ are linear neural networks, so they are not powerful enough to learn sophisticated patterns. Training is sensitive to outliers because outliers change the domain of $F_D$. 
Suppose that $w=\frac{Au_j+b}{\|Au_j+b\|}$ and $v_j\in\{e_1,\dots,e_n\}$. Then the amplitude $\langle w,e_k\rangle$ is possibly negative which is paradoxical; our analysis indicates that the probability that $v_j=e_k$ should be
$\langle w,e_k\rangle^2$ but we know that there is a zero probability that $(u_j,e_k)$ belongs to the training data. The paradoxical nature of this observation is due mainly to the simplicity of the trained model. There is no closed form expression that tells us the local maximum of $F_D$ and we must train using gradient ascent which may be slow.


**Generalization**

Define a fitness function $F_{D,p}(A,b)$ by setting 
$F_{D,p}(A,b)=(\sum_{k=1}^{r}(\frac{|\langle Au_k+b,v_k\rangle|}{\|Au_k+b\|\cdot\|v_k\|})^p/r)^{1/p}$. Set $F_{D,0}(A,b)=F_D(A,b)$. 

Suppose that $e_1,\dots,e_n$ is again a basis for $V$ and that $v_k\in\{e_1,\dots,e_n\}$ for all $k$. 

Proposition: Suppose that $e_1,\dots,e_n$ is a basis for $V$ and $L(x)=\sum_{k=1}^n p_k(|\frac{\langle x,e_k\rangle|^p}{\|x\|})^{1/p}$. If $\langle x,e_j\rangle>0$ for all $j$ and $L(x)$ is locally maximized, then
$p_\alpha=\frac{x_\alpha^{2-p}}{x_1^{2-p}+\dots+x_r^{2-p}}$ for all $\alpha$.

Proof: Observe that $L(x)=\frac{(p_1x_1^p+\dots+p_rx_r^p)^{1/p})}{\|x\|}$, so $\log(f(x))=\frac{1}{p}\log(p_1x_1^p+\dots+p_rx_r^p)-\frac{1}{2}\log(x_1^2+\dots+x_r^2)$. Therefore,

$\frac{\partial}{\partial x_\alpha}f(x)=\frac{1}{p}\cdot\frac{p_a\cdot p\cdot x_\alpha^{p-1}}{p_1x_1^p+\dots+p_rx_r^p}-\frac{1}{2}\cdot\frac{2\cdot x_\alpha}{x_1^2+\dots+x_r^2}$.

Thus, $\nabla_X\log(f(x))=0$ precisely when $\frac{p_\alpha x_\alpha^{p-1}}{p_1x_1^p+\dots+x_rx_r^p}=\frac{x_\alpha}{x_1^2+\dots+x_r^2}$ for all $\alpha$. 

Therefore, there is some $\lambda$ where $p_\alpha x_\alpha^{p-1}=\lambda x_\alpha$. In this case, $p_\alpha=\lambda x_\alpha^{2-p}$. Since $1=p_1+\dots+p_r=\lambda x_1^{2-p}+\dots+\lambda x_r^{2-p}$, we know that
$\lambda=(x_1^{2-p}+\dots+x_r^{2-p})^{-1}$, so $p_\alpha=\frac{x_\alpha^{2-p}}{x_1^{2-p}+\dots+x_r^{2-p}}$.





