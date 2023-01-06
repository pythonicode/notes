# MATH 104: Matrix Norms & Inner Product

Recall the definition of norms, a map from a vector space $V \rightarrow \mathbb R$ 

Definition: Let $(V, \mathbb R)$ be a vector space, $||-||: V \rightarrow R$ is a norm if the following conditions hold:

1. $||x|| \geq 0$

2. $||x|| = 0$ if and only if $x = 0$

3. $||\alpha x|| = \alpha ||x||$

4. $||x + y || \leq ||x|| + ||y||$

We talked about norms in the space of real vectors, now we will talk about real matrices. The definition of matrix norm is the same, but we just need to find a norm that satisfies these properties.

### Matrix Norms

First idea: we can reshape a matrix into a vector by concatenating the columns.

Then the matrix norm can be equal to the vector norm of the flattened matrix.

Let's consider the 2-norm of a vector, what does it look like for a matrix?

Let $A \in R^{m\times n}$ and we flatten the matrix into a vector $\vec v =[a_1, a_2 \dots a_n]$ 

Then we take the 2-norm of $\vec v$ to get the *Frobenius Norm*of $A$.

$$
||A||_2 = \sqrt{\sum_{i=1}^m \sum_{j=1}^n a_{ij}^2}
$$

Also called the *F-norm* of $A$.



**Matrix p-norm**

Not the same way we calculated the F-norm. Definition:

$$
||A||_p = \max_{x\in \mathbb R^n} \frac{||A\vec x||_p}{||\vec x||_p}
$$

Recall from the homework that $||A||_2 = \max_\sigma$.

If $||\vec x|| = 1$ AKA $\vec x$ is a unit vector. Then we get $||A||_p = \max ||A \vec x||_p$

What about $||A||_1$?

$$
||A||_1 = \max_j \sum_{i=1}^n |a_{ij}|
$$

This is just the maximum column sum of the matrix (sum all columns and take max).

The counterpart is $||A||_\infty$

$$
||A||_\infty = \max_i \sum_{j=1}^n |a_{ij}|
$$

Which is the maximum row sum of the matrxi (sum all rows and take max).



**Examples**

Let $I_n$ be the $n \times n$ identity matrix. What is $||I_n||_F$?

Square of the entries of $I_n$ and take the square root: $||I_n||_F = \sqrt{n}$

What about $||I_n||_2?$ It's $1$ because max singular value of identity matrix is $1$.

What about general p-norm?

$$
||I_n||_p = \max_x \frac{||I_n\vec x||_p}{||\vec x||_p} = 1
$$

So any p-norm $||I_n||_p = 0.$

This type of norm is called an *operator norm*. The matrix is thought of as an operator on a vector $\vec x$ and geometrically can be thought of as the maximum change in magnitude of a vector after multiplying by $A$.

We can define:

$$
||A||_\alpha = \max_x \frac{||A \vec x ||_\alpha}{||\vec x||_\alpha}
$$

We can use different norms too, so the operator norm is defined as:

$$
||A||_{op} = \max_x \frac{||A \vec x||_\alpha}{||x||_\beta}
$$

Defined on some $\alpha$ and $\beta$.



**Definition: Consistency**

If a norm $||-||$ defined for all matrices (of any shape) satisfies: $||AB|| \leq ||A|| * ||B||$ for any such $A, B$ then the norm is called consistent. 



**Theorem:** all operator norms defined by $||A|| = \max_x \frac{||A\vec x||}{||\vec x||}$ are consistent $(\alpha = \beta)$.

How do we prove it? 

$$
||AB|| = \max_x \frac{||AB \vec x ||}{||\vec x||} = \max_x \frac{||AB \vec x ||}{||\vec Bx||} \frac{||B \vec x ||}{||\vec x||}  
$$

$$
= \max_x \frac{||A \vec y ||}{||\vec y||} \frac{||B \vec x ||}{||\vec x||} \leq \max_x \frac{||A \vec y ||}{||\vec y||} \max_x \frac{||B \vec x ||}{||\vec x||}  
$$



### Inner Product

Extending the definition of inner product for real and complex vectors.

Let $(V, \mathbb R)$ be a vector space. Then if we have a map $<-, ->: V\times V = \mathbb R$. 

This is a function that takes two vectos from vector space $V$ and outputs a real number.

The operation is called an *inner product* if:

1. $< x,  x> \geq 0 $ and $<x , x> = 0$ only if $x = 0$

2. $<x, y> = <y, x>$

3. $<x, ay_1 + by_2> = a<x, y_1> + b <x, y_2>$

If we have this inner product defined on $V$ then it is called an *inner product space.*



**Examples**

Simplest vector norm, in vector space $\mathbb R^n$ we can define $<x, y> = x^\top y$.

This is called the *Euclidean inner product*.

We can define the *weighted inner product* in $\mathbb R^n$ by $<x,y>_Q = x^\top Q y$ where $Q$ is positive definite. 

For a matrices $A, B \in \mathbb R^{m \times n}$ then $<A, B> = tr(A^\top B)$.

How do we show the above holds? First we need to show $tr(A^\top B) = tr(B^\top A)$. We already know generally that $tr(V) = tr(V^\top)$ so $tr(A^\top B) = tr((A^\top B)^\top) = tr(B^\top A)$.

We alos need to show that $<A, aB_1 + bB_2> = a<A, B_1> + b<A, B_2>$. We can use the linearity of traces to show this.

Finally we need to show $tr(A^\top A) \geq 0$. We can write the trace of $A^\top A$ as...

$$
tr(A^\top A) = \sum_{i=1}^m b_{ii} = \sum_{i=1}^m \sum_{j=1}^n (a_{ii})^2 = ||A||_F
$$

$$
b_{ii} = a_{1i}^2 + \dots a_{mi}^2 \geq 0
$$

Recall the vector space $C([0, 1], \mathbb R)$, continuous functions over $[0, 1]$.

We can have the inner product $<f, g> = \int_0^1 f(x)g(x)dx$.

We can define the space $C'([0,1], \mathbb R)$ which is the set of continuous functions over [0,1] with its derivative is also continuous over [0,1]. Then $<f, g> = \int_0^1 f'(x) g'(x)dx$ is not an inner product! Can you see why?



Theorem: $<-,->$ is an inner product on $V$. Then $||x|| = \sqrt{<x,x>}$ is a norm on $V$. The norm has 3 conditions, the first 2conditions are trivial so we just need to prove the triangular inequality.

$$
||x + y|| \leq ||x|| + ||y||
$$

$$
\sqrt{<x+y, x+y>} \leq \sqrt{<x,x>} + \sqrt{<y,y>}
$$

$$
<x+y, x+y> \leq <x,x> + <y,y> + 2\sqrt{<x,x>}\sqrt{<y,y>}
$$

$$
<x,x> + <y,y> +2<x,y> \leq RHS \text{ above}
$$

$$
<x,y> \leq \sqrt{<x,x><y,y>}
$$

Now use the Cauchy Schwanz Inequality to show that this holds.
