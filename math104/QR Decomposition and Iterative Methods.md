# MATH 104: QR Decomposition and Iterative Methods

### QR Decomposition

Given two vectors $a_1$ and $a_2$, we choose a $u_1 = a_1$. How do we find $u_2 \perp u_1$? A linear combination of $a_1$ and $a_2$. We use projections to find $u_2$.

If we project $a_2$ onto $a_1$, then subtract that component from $a_2$ then we get a $u_2$ that is orthogonal to $u_1$. So now $u_1 = a_1$ and $u_2 = a_2 - P_{u_1} a_2$ or $a_2 = a_2 - \frac{a_2 \cdot u_1}{u_1 \cdot u_1} u_1$ because it is vector projection. What if we have an $a_3$? We subtract the projecetion of $a_3$ onto $u_1$ and $u_2$ from $a_3$ to create $u_3$ that is orthogonal ot $u_1, u_2$. So $u_3 = a_3 - \frac{a_3 \cdot u_1}{u_1 \cdot u_1} u_1 - \frac{a_3 \cdot u_2}{u_2 \cdot u_2} u_2$

Now $u_1, u_2$ and $u_3$ form an orthogonal basis in  $span(a_1, a_2, a_3)$. 

This is the Gram Schmidt process. $u_k = a_k - \frac{a_k \cdot u_{k-1}}{u_{k-1} \cdot u_{k-1}} u_{k-1} \dots$

If a vector $a_i \in span(a_1 \dots a_{i-1})$ then $u_i = 0$.

( Example in class )

This can be applied to general matrices $A = \mathbb R^{m\times n}$.  Where $Q \in \mathbb R^{m \times m}$ and $R \in \mathbb R^{m \times n}$ this yield the correct dimensions from $A = QR$. This works well for tall matrices and we can simplify $Q$ and $R$ into smaller matrices because many rows of $R$ will be equal to 0.

Split $Q = [Q_1, Q_2]$ and $R  = \begin{bmatrix}R_1 \\ R_2 \end{bmatrix}$. Where $Q_1 \in \mathbb R^{m \times n}$ and $R_1 = R^{n\times n}$ where $A = Q_1 R_1$. We can throw out $Q_2$ and $R_2$ because all values in $R_2$ are 0.

We find $Q_1$ and $R_1$ using the same process, Gram Schmidt. Finding $Q_2$ is not easy.

Example: Find a QR decompositions for the following matrix:

$$
A = \begin{bmatrix} 1& 1 \\ 2 & 1 \\ 0 & 3 \\ 1 & 0 \end{bmatrix}
$$

### Iterative Methods

If $x_{k+1} = f(x_k)$ then it is an iteration.

If we take $\lim_{k \to \infty} x_{k+1} = \lim_{k \to \infty} f(x_k)$

The limit of an iteration converges when $x^* = f(x^*)$.

**Jacobi Method** the details are beyong the scope of this class but the basics are:

$A = D + L + U$ where $D$ is the diagonal of $A$, $L$ is the lower triangular part of $A$ and $U$ if the upper triangular part of $A$. 

Now we have $(D + L + U)x = b$ so $Dx = b - Lx - Ux$ and $x = D^{-1}(b - Lx - Ux)$

Iteration scheme is $x_{k+1} = D^{-1}(b - Lx_k - Ux_k)$.

**Gauss-Seidel**

$(D + L)x = b - Ux$ so the iteration scheme is $x_{k+1} = (D+L)^{-1} (b - Ux_k)$


