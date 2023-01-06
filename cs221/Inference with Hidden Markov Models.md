# CS221: Inference with Hidden Markov Models

Hidden Markov Models, super influential technology in many different fields.

Object tracking - working with noisy data and making predictions with probabilities.

HMMs are a more interpretable and controllable way to do object tracking then just using a large neural network.

Given a bunch of noisy data of where the object was at the previous timestep, where am I now?



### Forward Backward

There are two things we usually want to do with HMMs.

**Filtering** - given the emissions (data) from previous state, where am I now?

**Smoothing** - given a bunch of noisy data over a period of time, where was I?

Lattice Representation. Represent the HMM as a directed acyclic graph with weights on each edge as

$$
p(h_i | h_{i-1}) p(e_i | h_i)
$$

This is the *transition probability* x *emission probability*.

How do we solve for certain values? Use dynamic programming.

Forward messaging

$$
F_i(h_i) = \sum_{h_{i-1}} F_{i-1}(h_{i-1}) Weight(h_{i-1}, h_i)
$$

And backwards messaging

$$
B_i(h_i) = \sum_{h_{i+1}} B_{i+1}(h_{i+1}) Weight(h_i, h_{i+1})
$$

And our final solution is

$$
S_i(h_i) = F_i(h_i) B_i(h_i)
$$

Then we can get our EXACT inference solution:

$$
P(H_i = h_i | E = e) = \frac{S_i(h_i)}{\sum_v S_i(v)}
$$

with a big O runtime as

$$
O(n|Domain|^2)
$$

For the filtering question, we can ignore the backwards messaging which is only needed for smoothing.

Beam search to solve HMMs doesn't work too well because sometimes it gives bad results or sometimes it's very slow. What if we add some sampling/randomness to beam search?


### Particle Filtering

**Step 1: Propose**

Take a current partial assignment called a "particle" and generate a continuation of each particle by sampling the Markov chain dynamics to create a new particles.

**Step 2: Weight**

Weight the particles based on evidence. For each freshly sampled particle, see which particles are more likely by weighing with a probability $p(e_3 = 2 | h_3)$

**Step 3: Resampling** 

Look at the weights and normalize them to add to 1. Then resample with replacement from the new probabilities to create a "new generation" of particles for the next round of proposals. 

The Algorithm:

```python
Initialize C = [{}]
for i in range(n):
    # propose
    C' = { h and h_i given h in C and h_i sampled from p(h_i | h_i-1) }
    # weight 
    I didn't have time to copy the slides, but cs221.stanford.edu
```

The goal is to solve the filtering problem which is $P(H_3 | E_1 = e_1, E_2 = e_2, E_3 = e_3)$.

Recall Gibbs sampling which is very similar to Particle Filtering (sampling and trying to converge to a solution). Depends on variables being mostly independent and too slow for HMMs where the variables depend on each other.



Conclusion:

Forward Backward algorithm, an exact inference algorithm but quadratic time.

Particle Filtering, approximate sampling algorithm for inference w/ linear complexity.

Gibbs Sampling, modify complete assignments, also sampling and linear time.
