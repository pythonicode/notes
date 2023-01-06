# CS 221: Search and Conditional Independence

Quick review of CSP, the goal is to assign values to a set of variables $X$ where $X_i \in Domain_i$. 

An assignment $x$ has a weight based on the constraints or "factors" $f_i$

Example: Object Tracking

Noisy sensors report positions and objects can't teleport. What trajectory did the object take? Let's model the problem as  a CSP.

Variables $X_i \in \{0, 1, 2\}$

Observation factors $o_i(x_i)$ noisy information about the position.

Transitions factors $t_i(x_i, x_{i+1})$ object positions can't change too much each step.

Variables are discrete for now, but can be made continuous with different methods.

### Beam Search

Backtracking DFS is still exhaustive and can grow exponentially despite AC-3 Lookahead. Instead, we can use a greedy search: pick the best possible variable assignment at each step. This often does *not* find the optimal assigment, it is suboptimal because picking the best assignment now doesn't guarantee the best overall assignment, we may have to make a suboptimal assignment now to get the best optimal overall assignment.

The Beam Search algorithm is a form of greedy search with more than 1 candidate that we are keeping track of. At each step, we expand our search by expanding the number of potential assignment for the next variable. Once the number of candidates exceeds our "beam width" $K$ then we prune our candidates to the best $K$ candidates.

```python
K = 4
C = [{}] # candidate list
for i in range(1, n):
    C' = extend each candidate in C
    prune C' to max K elements
```

Using beam search, we are more likely to find the optimal candidate than basic greedy search and we are more likely to find a more optimal solution than basic greedy search.

What is the complexity of beam search? $O(nKb \log K)$ which is way better than $O(b^n)$.



### Local Search

For now we've seen backtracking and beam search where we extend partial assignments (AKA build the house from the bottom up).

Local search is where we modift complete assignments.

The key idea: start with a suboptimal solution and improve it until we get a good solution.

Take small steps, say we start with an assignment $x$. We can modify one variable $X_i \in x$ until it gets a higher value then we set $X_i$ to a new value and get a new assignment $x'$.

Exploiting locality, if I'm updating a variable assignment for variable $X_i$ then I only care about factors that depend on $X_i$.

```python
# Iterated Conditional Modes
initialize x as a random assignment
while x has not converged
    for i in range(1, n):
       update x[i] to the best value
```

ICM has the same problem as Greedy search where it can get stuck at a suboptimal solution. However we can run ICM multiple times and pick the best solution to make it more likely to find the global optimal solution as long as we are randomizing the initial assignment.



### Gibbs Sampling

A modified version of ICM that is probabalistic.

```python
initialize x as a random assignment
while x has not converged
    for i in range(1, n):
       set x[i] = v with probability P(X[i] = v | X[!i] = x[!i])
       increment count(x[i])
estimate P(X[i] = x[i]) as count(x[i])/sum([count[v] for v in domain(X[i]))
```

In practice Gibbs sampling works a lot better than ICM, helps use get out of local minima and if we compute merginals we can converge to a correct / mostly optimal solution.

Can be thought of as a stochastic exploration of variable assignments.



### Conditioning

Motivation, using a graph we can exploit locality. If a graph is really simple then it is easy to search. If we are able to turn a fully connected contraint graph into a simpler one, then we can simplify the problem

Independence. If a variable $A$ and another variables $B$ do not have any path connecting them then they are independent. We can also have a subset of variables $U$ and another subest $V$ that are independent from each other.

We can use independence (or partial independence) to speed up our algorithms by separating out the graph.

Say for example we have a map coloring problem and we conditon on certain parts of the map (certain states, countries etc). Main idea: set a variable $X_i = something$ then remove $X_i$ and add the new factors that account for the assigned value of $X_i$.

**Conditional Independence**

 Let $A, B, C$ be a partitioning of variables. We say $A$ and $B$ are conditionally independent given $C$ if conditioning on $C$ produces a graph in which $A$ and $B$ are independent.

$A \perp B \mid C$.

**Markov Blanket**

How can we sepearate an arbitrary set of nodes from everything else? Take a set of nodes and then take all its neighbors then that's called the Markov blanket. A markov blanket can generate conditional independence given a group of variables $A$.


