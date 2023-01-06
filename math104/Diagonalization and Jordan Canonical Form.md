# MATH 104: Diagonalization and Jordan Canonical Form

Recall from the previous lecture, a real symmetric matrix $A$ is orthogonally similar to a diagonal matrix $D$. 

### Schur Canonical Form

Let $A \in \mathbb C ^{n \times n}$ then there exists a unitary matrix $U$ and an upper triangular matrix $T$ where:

$$
U^H A U = T\text{ or } A = UTU^H
$$

By Induction, if the result holds for $n$ then we consider the case $n+1$.

Let $A \in \mathbb C^{(n+1)\times (n+1)}$ and let $\lambda$ be an eigenvalue of $A$ with a corresponding right eigenvector $x$. Let's find an orthonormal basis of $\mathbb C^{n+1 \times n+1}$ with vectors $X = [x, x_1, \dots x_n]$ or $X  = [x, X_2]$. Now calculate $X^H A X$ and we find that we get the matrix:

$$
\begin{bmatrix} \lambda & x_1^H A X_2 \\ 0 & X_2^H A X_2 \end{bmatrix}
$$

Theorem: If $A \in C^{n \times n}$ is it unitary similar to a diagonal matrix if and only if $AA^H = A^HA$ then $A$ is called a normal matrix.

If $A$ is diagonalizable than $A = UDU^H$ and $UDU^H UD^H U^h = UDD^H U^H$ and $U^HD^HUU^HDU = \dots$.



### Jordan Canonical Form

A similarity transformation result. NOT an orthogonal or unitary similarity transformation, but a general matrix transformation.

For any matrix $A \in \mathbb C^{n \times n}$ let $\lambda_1 \to \lambda_n$ be eigenvalues of $A$. Then there exists an invertible matrix $X \in \mathbb C^{n \times n}$ such that

$$
X^{-1} A X = diag(J_1, J_2, J_3 \dots)
$$

$$
J_k = \begin{bmatrix} \lambda_i & 1 & 0 & 0 \\ 0 & \lambda_i & 1 & 0 \\ \dots \\ \dots\end{bmatrix}
$$

Each $J$ is called a "jordan block". What does Jordan Canonical Form tell us? Eigenvalues, multiplicity and characteristic polynomial.

(Examples in class)

What is the geometric meaning of Jordan Canonical Form?

Take a jordan block $J$ then we can get the corresponding columns $X_J$ and we know that 

$$
AX_J = X_J J
$$

So $Ax_1 = \lambda x_1$ and $Ax_2 = x_1 + \lambda x_2$ etc.

What does this mean?

$$
(A - \lambda I)^k x_k = 0
$$

So each vector $x_k$ in the jordan block is in the nullspace $N((A-\lambda I)^k)$.

We have a name for these $x_k$ vectors which is called a *right principle vector of degree k*.

How do we compute the Jordan Canonical Form of a matrix $A$?

1. Find all the eigenvectors $x_1 \to x_r$ where $r \leq n$.

2. For each $x_i$ starting with $x_i^1 = x_i$ solve $(A-\lambda I)x_i^{k+1} = x_i^k$

3. Stop when $x_i^k \in span(x_i^1 \dots x_i^{k-1})$

`
