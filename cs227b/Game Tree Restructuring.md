# CS227: Game Tree Restructuring

Techniques so far: Grounding game descriptions. Executing ground and/or symbolized descriptions. Optimizing ground decriptions e.g. dropping subgoals.

Techniques today: pruning games trees and decomposing game into independent subgames.

### Pruning Game Trees

"Multiple" games. Players play multiple of the same game simultaneously but some of them don't matter so how does the player know which ones don't matter?

Inertia - if you setup your propnet and don't change anything then nothing changes, inertia guarantees that if the actions in the propnet are not connected to a terminal node or a goal node then nothing is affected if we remove it.

Ultimate Return - 

Procedure:

1. Ground the game

2. Computer actions to goals, termination, legality

3. Prune actions that don't lead to goals

Okay, more specifically start with all of your goal facts and recurse back to find all the actions that affect goals. Then do the same with terminal facts and legality facts then any rules. Then update legal actions to only be the ones that lead to goals and terminal states.



### Game Factoring

"Best" games are similar to multiple games where it takes your best score out of many games. Can we decompose the whole game into independent subgames and combine the result of independent subgames?

Conditional Factoring - when two independent subgames occur during the game can you factor the game into independent subgames?

Bottlenecks - series of games each which must terminate before next begins.

Dead state elimination - find states that cannot lead to acceptable outcomes.

Goal monotonicity - detect monotonicity in states (higher goal value in non-terminal states)




