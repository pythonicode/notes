# CS 221: Learning in Complex Games

### TD Learning Algorithm

Learn the value of every state in an MDP

$$
w = w - n [V(s, w) - (r + \gamma V(s'))] \nabla_w V(s, w)
$$

Useful for when we know the dynamics of the game, but we don't know the reward...

Slowly improve weights over multiple episodes, if you are playing the same game, then weights will learn good predictions in any state so the model can be run over multiple episodes and still learn good weights (sorry for confusing explanation).

TD Learning is very similar to Q-learning from the previous class:

**Q Learning** tries to estimate $Q_{opt}$ and learn how to act optimally in an environment.

**TD Learning** estimates the value of each state to learn $V_\pi$ typically an exploration policy, learns the value of a policy $\pi$



AlphaGo used these sort of algorithms to beat the world champion Go player.

Self-play (the model plays against itself) is a very common strategy for training these reinforcement learning agents.

If we know the Successor for each state (dynamics of the game), then TD learning allows us to leverage this rather than use Q-learning which doesn't know the transitions and is learning them by playing the game.



Important idea: function approximation to parameterize complex games.

Use weights and feature vectors or even a neural network.



### Simultaneous Games

Rock paper scissors (simultaneous) vs. Chess (turn-based)

What's the difference? Primarily, the game tree doesn't really make sense when there's no turns. So how to we represent a simultaneous game?

**Two-finger Morra**: Players A and B each show 1 or 2 fingers, if both show 1 B gives A 2 dollars, if they both show 2 then Player B gives A 4 dollars. If they show different numbers then player A gets 3 dollars from player B.

We can represent a simultaneous single-move game as a payoff matrix:

$$
\begin{bmatrix} A  & 1 & 2 \\ 1 & 2  & -3 \\ 2 & -3 & 4 \end{bmatrix}
$$

How do we evaluate the game? The value of the game if player A follows policy $\pi_A$ and player B follows $\pi_B$ then the value is $V(\pi_A, \pi_B) = \sum_{a,b} \pi_A(a) \pi_B(b) V(a,b)$ where V is the value matrix written above.

The challenge: player A is trying to maximize and player B is trying to minimize (game is still zero sum) how do they do so simultaneously?

Think about two-finger morra - if we write it as a turn-based game tree: going first is bad! We want to go after we have knowledge of what the other player did (single move)

For any fixed mixed strategy say $\pi_A = [1/2, 1/2]$ AKA randomly choosing 1 or 2 fingers. Then player B's best strategy can be attained by a pure strategy $\min_{\pi_b} V(\pi_A, \pi_B)$.

Here's the steps for finding the minimax value of a single move game:

Player A reveals a mixed strategy $\pi_A = [p, 1-p]$ where $p$ is a probability.

Then $V = \max_p \min(5p-3, -7p + 4) = -1/12$ (solve $5p-3 = -7p + 4$)

For every simultaneous two-player zero-sum game with a finite number of actions then

$$
\max_{\pi_A} \min_{\pi_B} V(\pi_A, \pi_B) = \min_{\pi_A} \max_{\pi_B} V(\pi_A, \pi_B)
$$

Revealing your optimal strategy does not hurt you when playing the game.



### Non Zero-Sum Games

The real world has some cooperation and some competition, not pure minimax or maximization. The easiest example of a non zero-sum game is prisoner's dilemma.

$$
\begin{bmatrix} A \cdot B & testify & refuse \\ testify & -5 \cdot -5 & 0 \cdot -10 \\ refuse & -10\cdot 0 &  -1 \cdot -1 \end{bmatrix}
$$

We need values for all players in the game based on what they play.

There is no longer an optimal play or minimax solution. Instead we have a **Nash equilibrium** which is a set of strategies $\{\pi^*_A, \pi^*_B\}$ for example where neither player has an incentive to change his/her strategy.

For example, in prisoner's dilemma, both players testifying is a Nash equilibrium because if either player deviates then they get a worse outcome.

**Theorem:** for an finite-player game with finite numbers of actions then a Nash equilibrium exists. There can be MULTIPLE Nash equilibria. The important thing to consider is that Nash equilibrium is weak compared to an optimal strategy.



### State-of-the-art in Game Playing

1997 Deep Blue defeated world champion Gary Kasparov

- Used fast computers to evaluate chess moves faster

- Alpha-beta search over 30 billion positions, depth 24 with singular extensions to a depth of 20

- Lots of domain knowledge includes in the algorithms

- Evaluation function with 8000 features

- 4000 "opening book" moves and all endgames with 5 pieces coded into the machine

- Learned from 700,000 grandmaster games

- Used a null-move heuristic (if the opponent moves twice then are they in a much better position or not much better)?



1990 Jonathan Schaeefer's Cinook defeated human champion.

- Ran on a standard PC

- Checkers had been completely solved with minimax, outcome is a draw with two optimal players playing against each other



With Backgammon and Go, there is a very large branching factor and we cannot solve with standard alpha-beta search.

Need to use learning to achieve great success (supervised learning and reinforcement learning). 

- Supervised learning where is looks at human games and learns good positions

- Reinforcement learning on self-play games

- Evaluation function: convolutional neural network

- Policy convolutional neural network

- Monte Carlo Tree Search



Other applications of Reinforcement Learning include security games, resource allocation, and language communication.


