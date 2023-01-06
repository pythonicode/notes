# CS221: Logical Models

State-based models $\to$ variable-based models $\to$ logic-based models

3 different types of models, before 1990s logic was dominant paradigm in AI.

In essence, logic was the way that we thought about intelligence, but that fell out of favor for probabalistic approaches and machine learning.

Problems with logical models:

1) deterministic and cannot handle uncertainty

2) rule based and don't allow for fine tuning from data

Strength: provides better expressivity

Personal assistants like Siri, Cortana or Alexa use logic models in practice.

How could we create a smart personal assistant? We want to tell the assistant a bunch of facts using natural language and be able to ask the agent questions about those facts.

It's hard to reason about natural language, there is a lot of ambiguity. This makes it hard to map logic and language. Semantic parsing is a difficult task, when hardfast rules are used its even more difficult, another reason logic systems fell out of favor.

Language is a mechanism for expression, natural language is informal while there is also formal language (like programming languages)

Important parts of logical languages

1) Represent knowledge about the world

2) Reason about that knowledge

Syntax defines a set of valid formulas, but we also need semantics to specift a set of models for each formula (assignments and configurations about the world). 

Inference rules, given a formula what new formulas can be added?



### Propositional Logic

We have propositional symbols (atomic formulas) $A, B, C$.

And we have logical connectives like "not", "and" "implies" etc.

A *model* in propositional logic is  truth values assigned to all the symbols in the model.

An interpretation assigns prepositional symbols given a formula (which is a logical connective)

A formula represents a set of models, $\mathcal M(f)$ is the set of models $w$ for which $\mathcal I(f, w) = 1$

All assignments that are consistent with the formula.

A knowledge base is a set of formulas and we want to find the set of allowable models given the knowledge base. Knowledge base specifies the constraints on the world while $\mathcal M(KB)$ is the set of all assignments that satisfy those constraints.

Entailment - given $Snow \cap Rain$ then we know $Rain$ is also true.

Contradiction - given $Snow \cap Rain$ and $!Snow$ then that's a contradiction

Contingency - a formula $f$ adds valuables information to our knowledge base

If the knowledge base entails $f$ then knowledge base contradicts $!f$.

If we are telling an agent a fact $f$ there are 3 situations

1 ) Entailment - agent already knew the fact

2 ) Contradiction - agent doesn't believe the fact

3 ) Contingent - agent will add that information to the knowledge base

If we are asking the agent a question it will answer

1 ) Entailment - yes

2 ) Contradiction - no

3 ) Contingent - I don't know

A knowledge base is satisfiable if $\mathcal M(KB) \neq empty set$

Given a satisfiability checker, running it twice can let us figure out if a formula is entailed, contradicted or contingent.

Checking satisfiability is the same as solving a CSP with the symbols as variables!

But we can do better! Exploit the fact that factors are formulas.

Inference rules have a framework:

$$
\frac{f_1, \dots f_k}{g}
$$

Where $f_1 \to f_k, g$ are formulas where $g$ is true given $f_1 \to f_k$ are true.

Algorithm (Forward inference)

```
Repeat until no change to KB
    choose a set of formulas f_1 to f_k in KB
    if matching rule exists:
        put g in KB
```

Inference rule defined entailed/true formulas AKA if we derive a formula form using a inference rule
