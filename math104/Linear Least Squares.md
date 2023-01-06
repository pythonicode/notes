# MATH 104: Linear Least Squares

Recall the definition of a linear equation: $Ax = b$. There is a solution to the equation when $b \in R(A)$. 

The Linear Least Squares problem is when $b \notin R(A)$ and we want to find the value of $x$ that makes $Ax$ closest to $b$. What is the closest point? The closest point is the orthogonal projection of $b$ onto $R(A)$. 

Find $x$ such that $||Ax - b||^2$ is minimized.

$$
\argmin_{x} ||Ax - b||
$$

What is the projection onto the range of a matrix? 

$$
P_{R(A)} b = AA^+b
$$

So we get the following equation

$$
Ax = AA^+b
$$

How do we solve it? Use the general formula for solution of linear equations.

$$
x = A^+AA^+b + (I-A^+A)y
$$

We get the following results if we use the SVD

$$
||Ax - b||^2 = ||SV_1^\top x - U_1^\top b ||^2 + ||U_2^\top b||^2
$$

So we are minimizing the first term.



### Matrix Least Squares

The matrix least squares problem uses the Matrix Frobenius norm

$$
\argmin_x ||AX - B || ^2_F
$$

This is equal to the sume of 2 norms of the column vectors of $X$ and $B$.

$$
||AX-B||^2_F = ||Ax_1 - b_1||^2 + \dots ||Ax_n - b_n||^2
$$

$$
\min ||AX-B||^2_F = \min ||Ax_1 - b_1||^2 + \dots \min ||Ax_n - b_n||^2
$$



### Minimal Norm Solution

Like linear equations, we can have many solutions to the least squared problem by adding any vector in the nullspace of $A$ to our solution because $Av = 0$ if $v \in N(A)$.

When we have infinitely many solutions which solution do we pick? The minimal norm solution, AKA the solution closest to the origin.

**Minimal Norm Solution**

The solution of the Least Squares problem with minimal 2-norm.

$$
\argmin_x ||x||^2
$$

For all solutions $x$ such that $Ax = P_{R(A)}b$

Theorem: For a Least Squares problem the minimal norm solution is $x = A^+ b$ and is a unique solution.



How do we find the minimal norm solution of the following equation?

$$
\argmin_X || AX - I ||_F^2
$$

We can extend the logic we used previously with the minimal norm solution for vector equations to matrices. So the minimal norm solution is.

$$
X = A^+I = A^+
$$



### Normal Equation

We don't want to find the pseudoinverse every time that we want to find the solution to a linear equation. Is there an easier way to do it? Yes!

Theorem: $x$ is the solution of the Least Squares problem $\argmin_x ||Ax-b||^2$ if and only if it is a solution of the following linear equation:

$$
A^\top Ax = A^\top b
$$

This is called the normal equation.

Proof: Let's define a residual $r = b - Ax$.

If $x$ is a solution of the Least Squares problem then we know that $r$ is minimized.

Also since $r$ is a projection onto the range of $A$ we know that $r \in R(A)^\perp$ and thus $r \in N(A^\top)$. So $A^\top r = 0$ and when we expand this we get the following:

$$
A^\top (b - Ax) = 0
$$

$$
A^\top b - A^\top A x = 0
$$

$$
A^\top A x = A^\top b
$$

That's the normal equation! Nice.


