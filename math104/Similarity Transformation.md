# MATH 104: Similarity Transformation

### Review of Linear Regression

Our goal is to find a line closest to a set of data points. $y = ax + b$.

To do this we need to choose a certain error to minimize. Typically we choose the residual squares which is why this is often solved using least squares.

Residual $e_1 = y_1 - (ax_1 + b)$

We can easily fit a line to pass through the point $(x_1, y_1)$ but there is a tradeoff of error between different points. So what are we trying to minimize? The sume of errors.

Minimize $e_1^2 + e_2 ^2 + \dots e_n^2$.

Thus we get $(y_1 - (ax_1+b))^2 + \dots (y_n - (ax_n + b))^2$.

We can turn this into a matrix and vector combination and make it into a least squares problem.

$$
Y = \begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{bmatrix}
X = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix}
\mathbb 1 = \begin{bmatrix} 1 \\ 1 \\ \vdots \\ 1 \end{bmatrix}
$$

So we can write the solution as

$$
||Y - (aX + b1)||^2
$$

$$
= ||[X, 1]\begin{bmatrix}a\\ b \end{bmatrix} - Y || ^2
$$

How do we solve for $a,b$? Use the normal equation!

$$
A^\top A x = A^\top b
$$

Where we have $A = [X, 1]$ and $x = \begin{bmatrix}a \\ b \end{bmatrix}$ and b = $Y$

For 2-dimensional data points, this turns into a very easy equation to solve.

$A^\top A \in \mathbb R^{2\times 2}$ and $x \in \mathbb R^2$ and $A^\top y \in \mathbb R^2$

For multi regression, with n-dimensional data points, it's still pretty easy to solve the system.



### Similarity Transformations

Let $A, B \in \mathbb R^{n \times n}$. Then $A$ is orthogonal similar to $B$ if there exists an orthogonal matrix $P$ such that $P^\top A P = B.$ (This is a similarity transformation on $A$)

The question is, can we use similarity transformations to simplify a matrix?

Theorem: Let $A \in \mathbb R^{n\times n}$ be symmetric. Then $A$ is orthogonally similar to a diagonal matrix $\Lambda$ which has its entries as the eigenvalues of $A$ (recall that a symmetric matrix $A = S\Lambda S^\top$)

Proof: if $n = 1$ then $A \in \mathbb R^{1 \times 1}$ then we have a trivial decomposition $A = [1][a_{11}][1]$.

Assume that an $n \times n$ symmetric matrix can be decomposed into $S \Lambda S^\top$. We will show that an $n + 1 \times n + 1$ symmetric matrix can also be decomposed.

Let $\lambda_1 \to \lambda_{n+1}$ be the eigenvalues of the matrix. Let $x$ be an eigenvector corresponding to the eigenvalue $\lambda_1$. Then $Ax_1 = \lambda_1 x_1$. Given the vector $x_1$ let's form an orthormal basis for $\mathbb R^{n+1}$ which is $\{ x_1, x_2 \dots x_{n+1} \}$. Then if we call $X = [x_1, x_2 \dots x_{n+1}]$ then we can create the matrix $X_2 = [x_2 \dots x_{n+1}]$ and $X = [x_1, X_2]$. t

$$
X^\top A X = \begin{bmatrix} \lambda_1 & 0 \\ 0 & X_2^\top A X_2 \end{bmatrix}
$$

Then by induction we can show that $X_2^\top A X_2$ is symmetric and $n \times n$ so we can use above to show that a $n + 1 \times n + 1$ matrix can also be decomposed.


