# CS 221: Adversarial Games

State based models: Search, Markov Decision Processes, Adversarial Games

A game with two players who are playing AGAINST each other.

**Example Game**

Player A chooses one of three bins. Player B chooses any number from the bin.

Player A wants the highest score and Player B wants lowest score.

### Game Trees

Each node in the tree is a decision point for a player. Each root-to-leaf path is a possible outcome of the game. Rewards are going to be at the bottom of tree.

The most common adversarial game - the *two-player zero sum game* 

$Players = \{agent, opp\}$

The idea of zero-sum is that one player is trying to maximize score and the other player is trying to minimize score, aka both players have opposite goals and do not cooperate.

Definiton of a two-player zero sum game is pretty similar to search except instead of having a cost function $Cost(s, a)$ we have a utility for each state (or all end states) $Utility(s)$ is the utility for $agent$ for the end state $s$. Then there is also $Control(s)$ or $Player(s)$ which is the player who is playing at state $s$.

For example: Chess.

$Players = \{white, black\}$

State $s$: position of all the pieces on the board

$Actions(s)$: legal moves that $Player(s)$ can make

$IsEnd(s)$: whether $s$ is checkmate or draw state

$Utility(s)$: +1 if white wins, 0 if draw and -1 if black wins



A lot of games don't have intermediate rewards which is why we represent all the utility at the end states $Utility(s) = 0$ is $!isEnd(s)$ for $s \in S$.

Another difficult thing is that different players have control at different states, not just dealing with randomness, but uncertainty of opponent's actions.



**The Halving Game**

Start with a number $n$ and player $A, B$ takes turns either decrementing $N$ or replacing $N$ with $N/2$ (these are the actions).

Every state has a player in control of the state so we can represent state as the following `state = (player, ...state_data)`

What does a policy look like in this game? Each player has their own policy $\pi_p(s)$ for player $p$ (we can easily swap it out for a stochastic policy $\pi_p(s,a) \in [0,1]$)

We can model MDPs as a game with a deterministic player against nature (a stochastic player).

A policy should take in a state and return an action.

```python
def simplePolicy(state):
    action = "decrement"
    return action
```



Say we have an agent policy $\pi_{agent}(s) = A$ and an opponent policy $\pi_{opp}(s,a) = 1/2$ for $a \in Actions(s)$.

We can calculate the expected value of nodes using the stochasticity of the opponent to calculate expected value of the two policies. Stochastic opponent is essentially equivalent to the MDP problem.

**Game Evaluation Recurrence**

We can evaluate the value of any state and return the value expected by running a certain policy.

How do we get a good player?



### Expectimax

Our agent will pick the action in a given state that will maximize the expected utility of the agent given a game tree.

![A game tree with expectimax values | Download Scientific Diagram](https://www.researchgate.net/profile/Jakob-Erdmann-2/publication/220174534/figure/fig1/AS:669989111595018@1536749260672/A-game-tree-with-expectimax-values.png)

Expectimax is the best possible policy that our agent can play given that the opponent plays policy $\pi_{opp}(s)$ however we don't always have $\pi_{opp}$ so what do we do?



### Minimax

Assume that the opponent plays the worst possible move for the agent at every step. This works well for zero-sum games because this is what your opponent is trying to do usually if it is a strong opponent.

**Max Nodes:** value of a max node is the child node with the max possible value

**Min Nodes:** value of a min node is the child node with the min possible value

This is assuming we're playing against the best possible opponent.



Can define the recurrence of minimax similar to expectimax except the opponent is minimizing the utility.

$$
V_{minmax}(s) = \begin{cases} Utility(s) & \quad IsEnd(s) \\
\max_a V_{minmax}(Succ(s,a)) & \quad Player(s) = agent \\
\min_a V_{minmax}(Succ(s,a)) & \quad Player(s) = opp\end{cases}
$$

The minimax policies are easy to define. Agent picks the max utility and opponent picks the min utility.

What we notice about minimax is that in any zero-sum game, there is a way for one player to always win or the players will always draw and there is no in between.



**Playing Against Suboptimal Opponents**

Is $V_{minmax}$ optimal against suboptimal opponents if it plays as if the opponent is optimal? Well we know that $V(\pi_{max}, \pi_{min}) \leq V(\pi_{agent}, \pi_{min})$ and also $V(\pi_{max}, \pi_{min}) \leq V(\pi_{max}, \pi_{opp})$ for any $\pi_{agent}$ or $\pi_{opp}$ however for suboptimal opponent policy, the optimal policy is NOT the max policy, but an expecitmax policy designed to play against $\pi_{opp}$.



What if we have an adversarial game with randomness? Mega-uncertainty!



### Expectiminimax

3 different types of nodes

1. Max Nodes

2. Chance Nodes

3. Min Nodes

Works almost the same with just minor adjustments to the recursion which includes a scenario for chance nodes that calculates the expected value over its children.

We can extend this to many different scenarios, for example... multiple opponents, different turn-taking structure etc.



Our core goal is to evaluate our best possible utility at the top of the game tree, however this is intractible for large games. Branching factor $b$ and depth $d$ takes $O(d)$ space and $O(b^d)$ time and with chess $b \approx 25$ and $d \approx 50$.



### Speeding Up Minimax

**Evaluation Functions**

Use heuristics! Create some evaluation function $Eval(s)$ that is a heuristic for the utility of state $s$. Start with a max depth called $d_{max}$

$$
V_{minmax}(s, d) = \begin{cases} Utility(s) & \quad IsEnd(s) \\
Eval(s) & \quad d = 0 \\
\max_a V_{minmax}(Succ(s,a), d) & \quad Player(s) = agent \\
\min_a V_{minmax}(Succ(s,a), d-1) & \quad Player(s) = opp\end{cases}
$$

The $Eval(s)$ function is estimating $V_{minmax}(s)$ however if it doesn't estimate it perfectly then the minimax isn't necessarily optimal, but this can save a lot of time while searching. Uses domain knowledge to approximate accurately.



**Alpha-Beta Pruning**

Choose $A$ or $B$ where $A: [3, 5]$ or $B:[5, 100]$ 

Well, we definetly want to choose $B$ no matter what. Branch and bound. Maintain lower and upper bounds on values, if intervals don't overlap non-trivially then we can choose optimally without doing extra work to search.

Max nodes can store lower bounds and min nodes have upper bounds.



**Move Ordering**

What ordering of nodes do we expand? Worst ordering of nodes is no improvement compared to normal minimax. However, the best ordering is $O(b^{0.5d})$ which is a major improvement. Random ordering even has a major improvement on normal minimax.

In practice, we can use the $Eval(s)$ function to order which nodes are chosen to search first (max nodes search node with highest $Eval(s)$ and vice versa for min nodes).




