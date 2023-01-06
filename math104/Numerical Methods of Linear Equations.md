# MATH 104: Numerical Methods of Linear Equations

Finding solutions by hand of large systems (matrices of 100x100 for example) is not possible and we need assistance of computers. 

Let's consider the general case $A \in \mathbb R^{n\times n}$ and $Ax = b$. We can find the inverse of the matrix $A^{-1}$ and then $x = A^{-1}b$ but the inverse if really difficult to find. The simplest case is if $A$ is a diagonal matrix, then we just have a bunch of scaled values of the entries of $b$.

Another pretty easy case is if $A$ is triangular. This is because we immediately get a cascading set of solutions.

$$
A = \begin{bmatrix} a_{11} & 0 & 0 \\ a_{21} & a_{22} & 0 \\ a_{31} & a_{32} & a_{33} \end{bmatrix}
$$

Then $Ax = b$ we know that $a_{11}x_1 = b_1$ so we've already solved for $x_1 = \frac{b_1}{a_{11}}$.

Another easy matrix to work with is the orthogonal matrix. If $A$ is an orthogonal matrix then it's really easy to solve $Ax = b$ because $A^{-1} = A^\top$ so $x = A^\top b$ really simple!

### Factorization Methods

Decompose our coefficient matrix into the product of several simpler matrices.

**LU-decomposition** 

The matrix $A$ is decomposed into a lower triangular matrix $L$ and an upper triangular matrix $U$.

Any matrix $A \in \mathbb R^{n \times n}$ can be decomposed as $A = LU$. How do we solve this easily?

$Ax = b$ can be solved as $LUx = b$. Let $y = Ux$ and solve $Ly = b$ then solve $Ux = y$, two separate sets of linear equations, but both are easy to solve compared to the original matrix (most of the time).

How do we get the LU-decomposition though?

Gaussian Elimination - recall how we solve linear equations by hand... get the set of equations and see if we can eliminate variables by adding and subtracting them together.

This, at the end of the day, gets us a triangular matrix that we can use to solve the system using row operations.

Recall that row operations can be encoded by matrices, thus we can get the following by doing any number of row operations (2 operations in this example)

$$
(R_2 R_1) A = U
$$

Where $U$ is upper triangular and $R_1, R_2$ is lower triangular. 

So to solve we do the following:

$$
R_2 R_1 A x = R_2 R_1 b
$$

$$
Ux = L^{-1}b \text{ since } R_2 R_1 = L^{-1}
$$

Thus we don't have to do an inverse! We just find the row operations to find $U$ then given the row operations $R_1 \dots R_n$ we can solve with no inverse!

$$
Ux = R_nR_{n-1} \dots R_1b
$$

A method to find $L$ and $U$ called **rank decomposition.**

Given a matrix $A$ find a rank 1 matrix with the same entries on the first row and column of $A$. Then write matrix $A$ as a combination of the outer product decomposition $uv^\top$ and the difference between $A$ and $uv^\top$. Then repeat the process until we get the sum of outer products.

Then, once we have the sum of outerproduct decompositions.

$$
A = u_1v_1^\top + \dots u_n v_n^\top
$$

Then we get the $L=[u_1, u_2 \dots u_n]$ and $U=[v_1, v_2 \dots v_n]$. Collect the columns and we get $L$ then collect the rows and we get $U$. Simple method to calculate $L$ and $U$ by hand.

( Example in class with a 3x3 matrix $A$ )



**QR-decomposition** where the matrix $A$ is decomposed into an orthogonal matrix $Q$ and a matrix $R$ which is upper triangular.

How do we solve using $QR$ decomposition? $QRx = b$ so first solve $y = Rx$ and then $Qy = b$ where $y = Q^\top b$.

Let's think about $QR$ intuitively.

$Q = [q_1 \dots q_n]$ and $R$ is upper triangular and $A = [a_1 \dots a_n]$ column vectors.

We can solve $a_1 = r_{11} q_1$, $a_2 = r_{12}q_1 + r_{22}q_2$. etc.

How do we actually find this? Gram-Schmidt orthogonalization for the columns of A.

If $u_1 = a_1$ then $q_1 = \frac{u_1}{||u_1||}$.

Then for $u_2 = a_2 - proj_{u_1}a_2$ so $u_2$ is orthogonal to $u_1$ then $q_2 = \frac{u_2}{||u_2||}$.

Continue as follows: $u_3 = a_3 - proj_{u_2} a_3 - proj_{u_1} a_3$ and $q_3 = \frac{u_3}{||u_3||}.$

We can use this to find $q_1 \to q_n$

Recall that projection of one vector $a_k$ onto another $u_k$ is $\frac{u_k^\top a_k}{u_k^\top u_k} a_k$
