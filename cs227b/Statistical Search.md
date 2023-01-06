# CS 227B: Statistical Search

*Consider bringing masks to class especially when we're in Gates.*

Play out episodes of the game and see which ones are good.

### Monte Carlo Search

1. Optionally explore game graph to some level

2. Beyond this, explore to the end of the game

3. Propogate these values up to decide which action is best

Terminal state values are averaged together to determine the value of the node that the search started from.

It's fast because we are randomly making moves until the end of the tree, only taking 1 (or a few) paths down the tree. Branching factor is eliminated and space is small.

Provides guidance when other heuristics fail.

Problems - the search is somewhat optimistic (opponent doesn't act randomly) and the search does not utilize game structure in any useful way.

Adversary is very unlikely to make the same moves as your Monte Carlo samples.

Typical Monte-Carlo search just uses as many probes as possible without expanding.

### Monte Carlo Tree Search

A better version of statistical search than normal Monte Carlo Search.

The idea of probing to the end of the tree is common between the methods.

Expands the tree non-uniformly and basically is a blend of greedy and MCS.

The Four Steps of MCTS

1. Selection - first select a node to expand on the end of the tree (fringe)

2. Expand - add successors of the selected node to the tree

3. Simulate - do random probes to the end of the tree to get the value of new node

4. Backpropogate - value of the new node to the top of the tree

Let's do an example... (in class)

The MCTS formula for choosing a node:

$$
selectValue = \frac{node.utility}{node.visits} + C \sqrt{\frac{\ln{node.parent.visits}}{node.visits}}
$$

Multiplayer and singleplayer games have a different approach. Have to modify the formula because min nodes will be minimizing the value and max nodes maximize.
