# MATH 104: Linear Regression

Can I use a linear function to provide an estimate of $y$ given $x$? Is there a linear relationship between two variables.

We can roughly infer a linear relationship from a scatter plot.

<img src="https://upload.wikimedia.org/wikipedia/commons/b/be/Normdist_regression.png" title="" alt="Regression analysis - Wikipedia" width="253">

How do we use linear algebra to find coefficients $a$ and $b$ such that $y = ax + b$?

We have a lot of "data points" $(x_1, y_1)  \dots (x_n, y_n)$. Consider a line, we want the line to be very close to every data point. There is an error we want to minimize between the line and the data point called the *residual*. The difference between the point on the line $y_1' = ax_1 + b$ and $y_1$ so we want to minimize $(y_1' - y_1)^2$. The residual is $e_1 = (ax_1 + b) - y_1$ and we want to minimize $e_1^2$ and the same goes for all data points so we want to minimize $\sum_{i=1}^n e_i^2$ aka minimize the residual squared summed for each datapoint. That is our objective function!

$$
\min_{a,b} \sum_{i=0}^n (y_i - (ax_i + b))^2
$$

How do we solve it? As a least squares problem.

$$
\vec x = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} 
\vec y = \begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{bmatrix}
$$

$$
\sum_{i=0}^n (y_i - (ax_i + b))^2 = || \vec y - (a \vec x + b)||^2
$$

Recall how to solve the least squares problem $||Ax - b||^2$

$$
A^\top A x - A^\top b = 0
$$

### Normal Equation

The general solution:

$$
\begin{bmatrix}a \\ b \end{bmatrix}  = 
\frac{1}{n \sum_{i=1}^n x_i^2 - (\sum_{i=1}^n x_i)^2}
\begin{bmatrix} n\sum x_i y_i - (\sum x_i)(\sum y_i) \\ (\sum x_i^2)(\sum y_i) - (\sum x_i)(\sum x_i)(\sum(x_i y_i) \end{bmatrix}
$$

So we've solve the general case for data points of 2 dimensions $(x,y)$.

How do we solve when we have $y \in \mathbb R$ and $x \in \mathbb R^p$ and our datapoints are like $(x_{11}, \dots x_{1p}, y_1)$ etc.

We are fitting a linear function $y_i = a_1 x_{i1} + a_2 x_{i2} + \dots a_p x_{ip} + b$

Error is calculated similarly as

$$
\sum_{i=1}^n (y_i - (a_1 x_{i1} + a_2 x_{i2} + \dots a_p x_{ip} + b))^2
$$



### Generalized Linear Model

Often a linear model is not accurate, say if I want to predict someone's weight based on their height. Maybe weight depends height cubically like $weight = height^3$. Wait... this is a lot like a least squares problem if $x = height^3$ and $y = weight$.

Key idea: $y$ doesn't have to depend linearly on $x$ only on $a$ and $b$.

Here is the definition of the Generalized Linear Model:

$$
y = a_1 \phi_1(x) + a_2 \phi_2(x) + \dots a_n \phi_n(x) + b
$$

How do we solve $min_x ||Ax -b||^2$ numerically? It's the same as solving the normal equation $A^\top Ax = A^\top b$. Or we can use $QR$ decomposition.

$$
||Ax - b||^2 = ||Q_1R_1x - b ||^2
= ||R-1 x - Q_1^\top b||^2 + ||Q_2^\top b||^2
$$

To solve we just need to find...

$$
R_1 x = Q_1^\top b
$$

And it has a minimum value

$$
||Q^\top_2 b||^2
$$


