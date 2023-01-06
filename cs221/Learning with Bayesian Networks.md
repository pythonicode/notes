# CS221: Learning with Bayesian Networks

One variables $R$ representing the rating of a movie where $R \in \{1,2,3,4,5\}$.

We are estimating the probabilities $p(1), p(2), p(3)$ etc.

How do we get this probability? Just counting! We have a training dataset $D$ where $D = \{1,3,4,5,5,1\}$ so if we want to find $p(4)$ we count $1$ occurence of the number $4$ in the dataset of size $6$ to $p(4) = 1/6$. Super easy!

Let's think about a more complicated Bayesian network.



### Maximum Likelihood

$G \in \{ drama, comedy \} R \in \{ 1,2,3,4,5 \}$

We create the network where rating depends on the genre. $\mathbb P(G = g, R= r) = p_G(g)p_R(r \mid g)$. Now how do we find the conditional distribution $p_G$ and $p_R$. It's still just counting! Wow so easy.

Now let's make the Bayesian Network even more complicated! Let's have a new variable $A \in \{0, 1\}$ whether the film won an award.

Here we run into a problem. When we condition on many things at once it becomes harder and harder to estimate the conditional probability distributions.

The Bayesian learning network is that same regardless of the network. We count and normalize to a distirbution and we solve the problem. Super easy!

Parameter tying, say you have two parameters that depend on the same parent condition. We can combine the variables into one variable and just counting them.

Example: Naive Bayes, the idea of building a graphical model where the latent variable is the think you want to predict and our data are a set of examples ( predict genre based on movie review ). We can tie together words regardless of position by just using word counts.

Another example: HMMs where transitions are the same so you can tie the parameters together. 

In all of these cases we've been dealing with the supervised case, as if we have exact data about the object of interest but often we don't.

Algorithm for maximum likelihood:

```python
for x in train:
    for x_i in x
        increment count(x_parents, x_i)
normalize to probability distributions
```

The intuition of maximum likelihood: we want to maximize the likelihood that our prediction matches the training data.



### Laplace Smoothing

There is a problem with Maximum Likelihood, given a coin that we flip once and get heads. What is the likelihood that we get heads? Based on maximum likelihood, the probability of heads $p(H) = 1$.

With smaller amounts of training data then maximum likelihood falls apart. It's too aggressive in trying to maximize likelihood of the training data, but what we really want to maximize is the likelihood of the test data.

We can modify Laplace smoothing by doing "pseudo counting". We start with a prior belief then modify it with our examples. Can be modified with a constant $\lambda$ term.

The most common prior to use it assign a small probability of observing EVERY possible outcome. Add the constant $\lambda$ to the counts and do everything else as normal.



### Unsupervised Learning with EM

What happens if we don't observe some of the variables? Maximum marginal likelihood.

Let's say some variables $H$ are hidden and others are observed $E$.

Essentially, we can ignore the hidden parts and find maximum likelihood over the observed parts.

Expectation Maximization: generalization of K-means algorithm where $H$ is hidden and $E = e$ is observed. The algorithm, we alternative between 2 steps, E-step and M-step.

```
Initialize parameters
E-step:
    Compute q(h) = P(H = h, E = e) for each h
    Create weighted points (h,e) with weight q(h)
M-step
    Compute maximum likelihood to get parameters
Repeat until convergence
```



### Conclusion

The paradigm we learned tofay was learning with maximum likelihood (learning parameters of a bayesian network). Improvements like LaPlace smoothing and Expectation Maximization can help address some of the drawbacks of maximum likelihood.
