# CS227B: Grounding

FIrstly, MCTS and MCS isn't always great.

We aren't getting that many depth charges, why? It's slow for some games like Skirmish, but tend to get better as the game goes on.

### Metagaming

Match-independent game processing, done independent of any particular opponent or state. Objective of metagaming is to optimize performance in playing specific matches of the game.

Usually done during the start clock or between moves or in parallel with the game.



**Boring Methods:** Headstart on Game Tree Search, Endgame Book

**More interesting:** Game Grouding ("propnets"), Game Reformulation, Symbolic Reasoning.



### Game Grounding

The process of instatiating game rules by replacing all variables by ground terms.

**Symbolizing** is the process of replaceing ground propositions by atomic symbols.



**Example**

Take a rule with variables e.g. 

$row(A, R) : cell(A,R)$

turns into 

$row(1, x): cell(1,x)$

$row(2, x) : cell(2,x)$

etc.



So, the benefits are the ground decriptions are simpler, interpreting ground descriptions is more efficient time-wise.

There is a disadvantage, many more rules and not all games can be grounded in a reasonable amount of time.

Recall, base propositions. They are descriptions of every possible state that could be in the game. 

First, we can compute base properties:

$base(control(R)) :- role(R)$ 

can turn into the following:

$control(x) :- role(x)$

$control(o) :- role(o)$

The number of rules increases polynomially not exponentially like the game tree so usually this is useful.

Second, we compute actions similary, using the action propositions.

Third, we can add veiw propositions USING the base propositions we computed.

Fourth and finally, we need to instantiate operation rules.



**Execution**

We could replace our rules with the grounded rules and that's the only change, however we could make our interpreter work better with grounded / symbolized games.

General interpreter must allow for unification of expressions involving variables and it is expensive. Ground interpreter unifications are replaced by string equality which is much less expensive. Ground interpreters are still list, so if you symbolize the ground terms (turn them into pure strings) then the equality test is even cheaper.

If you've already grounded the terms you might as well symbolize them! Pretty easy.

Implementation (covered on slides in class).

Ground interpreter sometimes plays slower. Why? If you use the normal interpreter, often times the incrase in the number of rules makes it slower than if we use the normal non-grounded rules.



### Propositional Nets

Propositions, connectives and transitions. Can model a game as a prop net by using these devices in a graph or combinational circuit. Any grounded symbolized game can be turned into a prop net or vice versa. This is a super advanced general gameplaying strategy with crazy strategies that use FPGA.
