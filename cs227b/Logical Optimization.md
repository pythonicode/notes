# CS227B: Logical Optimization

Grounding some games is pretty much impossible, but there are some logical rules we could follow that makes the game a lot simpler.

The most valuable technique is called

### Subgoal Ordering

Given a rule solution(X,Y) :- p(X) & r(X,Y) & q(Y) using a standard interpreter if we reorder the the subgoals into solution(X,Y) :- p(X) & q(Y) & r(X, Y) then it will run much faster because the rules will be bounded.

It usually helps especially if the rules are written in a bad order.



### Subgoal Removal

Remove subgoals that don't matter. Pretty easy.



### Rule Removal

Remove redundant rules AKA rules where whenever another rule is true this rule is true so you can remove it because it's already covered.



### Materialization

Given certain rules can we modify things in the game description to get better performance? Difficult concept.



### Reformulation

Some games can have rules that are very expensive to run or even run forever (infinite loop) if the rules are written badly or something.

We can reformulate the rules at runtime to make our game player able to better interpret the rules (extremely hard).



### Theorem Proving

Idk this is tough stuff. cs227b.stanford.edu
