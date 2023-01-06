# CS221: Resolution and More Logical Models

Recall the inference algorithm for logic programs. Repeated apply inference rules to get new facts about the world. Modus ponens -> an example of an inference rule we can apply.

Recall if we use propositional logic with only Horn clauses and modus ponens then we get a sound and complete system. Can we do the same for all of prepositional logic (not restricted).

Yes! We can, it's called resolution.

### Resolution Inference

Horn clauses are relatively limiting, altough implications can be written with disjunctions.

$A \to C$ is the same as $!A \cup C$

Resolution inference rule, we use "cancelling out" of prepositions

$$
\frac{Rain \cup Snow, \quad !Snow \cup Traffic}{Rain \cup Traffic}
$$

How do we show soundness of resolution? If $Snow = 0$ then we know $Rain = 1$ so $Rain \cup Traffic = 1$ otherwise if we have $Snow = 1$ then we know $Traffic = 1$ so $Rain \cup Traffic = 1$.

A conjunctive normal form formula or CNF formula is a conjunction of clauses.

$$
(!A \cup B) \cap (!C \cup D)
$$

Proposition: any formula in propositional logic $f$ has a CNF.

How do we convert a formula to a CNF.

Remove implication with the rule above. $A \to C$ is the same as $!A \cup C$

Push negation inwards (de Morgans law) and simplify to get a CNF.

Algorithm: resolution based inference

Add $!f$ into the knowledge base, convert all formulas to CNF and repeatedly apply resolution inference rule.

If the final knowledge base is unsatisfiable we can conclude that $f$ is entailed by the knowledge base.

The problem with resolution is the time complexity. We can form arbitrarily large clauses that cause a lot more formulas to be put back into the knowledge base over and over again at each step.

### First Order Logic

There are many limitations in propositional logic.

How do we write the following:

*All students know arithmetic.*

*Every even integer greater than 2 is the sum of two primes*

We can't do that with first order logic! That's because there are uncountable objects. What's missing is predicates.

Some examples:

$Knows(alice, arithmetic) \cap Knows(bob, arithmetic)$

We have some new terms, constant symbols, variables and functions of terms.

$\forall x : Student(x) \to Knows(x, arithmetic)$

We have atomic formulas, connective and quantifiers.

Artomic formulas are a predicate applied to terms, connectives can be applied to formulas and quantifiers can be used to enumerate variables.

Universal quantifier, think conjunction: $\forall x P(x) = P(A) \cap P(B) \cap \dots$

Existential quantifier, think disjunction: $\exists x P(x) = P(A) \cup P(B) \cup \dots$

Be careful with connectives, sometimes it's easy to make a mistake mapping natural language quantifiers with their actual formula.

Graph representation of a model, if only have unary and binary predicates, a model can be represented as a directed graph.

When we talk about models for first order logic, we have some restrictions:

1) Unique names assumption, each object has at most one constant symbol.

2) Domain closure, each object has at least one constant symbol

Propositionalization, we can expand every knowledge base written in first order logic as a prepositional logic knowledge base.

**Inference Rules for First Order Logic**

We first will talk about definite clauses. 

$$
\forall x \forall y \forall z (Takes(x,y) \cap Covers(y,z)) \to Knows(x,z)
$$

A definite clause has variables $x_1, \dots x_n$ and atomic functions $a_1, .. a_k$ that may depend on the variables.

Modus ponens in first order logic. Doesn't work right away so we have to use substitution and unification. For example, substitute $x \to alice : P(x)$ and we get $P(alice)$.

Unifications find the "right" substitution that does the least amount of work.

Unification takes in two formulas $f$ and $g$ and returns a substitution that makes $f$ and $g$ the same if a valid substitution exists, and it's the least commital substitution.

We can unify the atomic formulae and the formulas in the quantifier expression to get a substitution to get us the output.

Time complexity of modus ponens inference is pretty bad. However, modus ponens is complete for first order logic with only Horn clauses.

It is also semi-decidable: 
