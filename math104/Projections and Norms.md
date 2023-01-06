# MATH 104: Projections and Norms

*Practice exams are now on Canvas, solutions will be uploaded later. Get an idea for the difficulty of the midterm exam next week.*

*Office Hours moved to Sunday Evening to Accomodate for the Exam, review the practice midterms in office hours and on lecture Monday morning.*

### SVD

Recall $A = U \Sigma V^\top = U_1 S V_1^\top$. You can compute the eigendecomposition, $AA^\top$ and $A^\top A$ to find $U$ and $\Sigma$ and $V$. Recall the problem from the homework, we get the matrices $\begin{bmatrix} 25 & 0 \\ 0 & 25 \end{bmatrix}$ and $\begin{bmatrix} 25 & 0 & 0 \\ 0 & 25 & 0 \\ 0 & 0 & 0 \end{bmatrix}$

There is a problem with this method: sometimes there is no unique choice for eigenvectors. The proper method is to do the eigendecomposition of **either** $AA^\top$ or $A^\top A$ to solve for either $U$ or $V$ and $\Sigma$ . Given $A = U_1 S V_1^\top$. 

We find that we can find $V_1 = A^\top U_1 S^{-1}$. 

### Projection

Recall $X = span(v_1 \dots v_k)$ and $V = [v_1 \dots v_k]$ then the projection matrix $P_x = VV^\top$, this is the orthogonal projection.

Let's find the orthogonal projection onto the 4 fundamental subspaces.

Basis for $R(A) = U_1$ so the projection is $U_1 U_1^\top$ or $AA^+$

Basis for $R(A)^\perp = U_2$ .... like above but $I - AA^+$

Basis for $N(A) = V_2$

Basis for $N(A)^\perp = V_1$ the projection: $A^+ A$

**Example**

Find $P_{R(A)} = AA^+$ 

$$
P_{R(A)} = \begin{bmatrix} 1/2 & 1/2 \\ 1/2 & 1/2 \end{bmatrix}
$$

And find $P_{N(A)} = I-A^+ A$

$$
P_{N(A)} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix} - \begin{bmatrix}1/2 & 1/2 & 0 \\ 1/2 & 1/2 & 0 \\ 0 & 0 & 0 \end{bmatrix}
$$

Okay not too bad.

### Norms

Recall vector norms, generalization of the length of vectors for $x \in \mathbb R^3$

$$
||x|| = x^\top x = \sqrt{x_1^2 \dots x_n^2}
$$

**Definition**

Let $(V, \mathbb R)$ be a vector space. $||x||: V \rightarrow \mathbb R$ is a norm if ...

1. $||x|| \geq 0$ for any $x \in V$ and $||x|| = 0$ only if $x = 0$.

2. $||\alpha x || = |\alpha| ||x||$ for any $x \in V$ and $\alpha \in \mathbb R$.

3. $||x + y|| \leq ||x|| + ||y||$ (triangular inequality)

We only need these three conditions! Then it's a norm. If we have a norm defined on $(V, \mathbb R)$ in this way then we call $V$ a *normed space*.

**Examples**

P-norms on $\mathbb R^n$ defined as $||x||_p = (|x_1|^p \dots + |x_n|^p)^{\frac{1}{p}}$

The most obvious examples is the 2-norm, also known as the *Euclidean norm* which is our conventional understanding of length.  The 1-norm is also sometimes seen.

$$
||x|| = |x_1| + |x_2| + \dots |x_n|
$$

Also known as the *Manhattan norm* or Manhattan Distance.

Another interesting norm is the *Infinity Norm*. AKA the limit as $p \rightarrow \infty$ of the p-norm which  becomes $\max_i |x_i|$. 

The 2-norm of $\begin{bmatrix} 3 \\ 4 \end{bmatrix}$ is 5, 1-norm is 7 and $\infty$ norm is 4.

Another type of norm is the *weighted 2-norm*.

$$
||x||_Q = \sqrt{x^\top Q x}
$$

Where Q is a positive definite. If $Q = I_n$ then it's just normal 2-norm.

How do we show that triangular inequality holds?

$$
||x + y||_Q \leq ||x||_Q + ||y||_Q
$$

Decompose $\Lambda = \Lambda^{1/2} \Lambda^{1/2}$ then use the 2-norm which has triangular inequality.

Let $V = C([0,1], \mathbb R)$ where $C(X, Y)$ is continuous functions with domain $X$ and range $Y$.

For $f(x) \in V$ then $||f(x)|| = \max_{x} |f(x)|$

**Properties of p-norm**

Holder inequality - for $x, y \in \mathbb R^n$ and $1/p + 1/q = 1$ we have $|x^\top y| \leq ||x||_p ||y||_q$

Cauchy-Schwaz Inequality - $|x^\top y| \leq ||x||_2 ||y||_2$

Easy way to prove Cauchy-Schwaz Inequality is using the equation for $cos(\theta)$

We can use Holder Inequality to show that for $x \in \mathbb R^n$

$$
||x||_1 \leq n^{1 - \frac{1}{p}} ||x||_p
$$

**Equivalence of Norms**

Two norms $||-||_a$ and $||-||_b$ on $V$ are equivalent if there exists $c_1 , c_2 \in \mathbb R$ such that $c_1 ||x||_b \leq ||x||_a \leq c_2 ||x||_b$

**Theorem:** all norms in $\mathbb R^n$ are equivalent.

Let's try to show that $||x||_1$ and $||x||_\infty$ are equivalent.

$$
||x||_1 = |x_1| + \dots |x_n|
$$

$$
||x||_\infty = \max_i |x_i|
$$

How can they be equivalent? Notice if we pick $c_1 = 1$ then $||x_1|| \geq c_1||x||_\infty$  and if we pick $c_2 = n$ then $||x||_1 \leq n \max_i |x_i| = c_2 ||x||_\infty$ so they are equivalent!
