---
title:
- Reading 3A - Elements of Finite Model Theory
author:
- Tyler Hanks, Richie Yeung
theme:
- Copenhagen
date:
- Apr 24, 2023

---

# Chapter 1: Introduction
* Finite model theory studies the expressive power of logics on finite models.
    * Finite graphs
    * Finite strings ...
* Classical model theory, on the other hand, concentrates on infinite structures
    * $\langle\mathbf{C}, +, \cdot\rangle$
    * $\langle\mathbf{R}, +, \cdot, <\rangle$
    * Infinite graphs ...

# Chapter 1: Introduction
Example 1: $NP$ vs $\exists SO$

<!-- Can't express reachability in FOL -->

### Hamiltonian Cycle
Given a graph $G = (V, E)$, is there a cycle that visits every vertex exactly once?

### 3 Colorability
Given a graph $G = (V, E)$, can we color the vertices with three colors such that no two adjacent vertices have the same color?

# Chapter 1: Introduction
Example 1: $NP$ vs $\exists SO$

::: {.block}
### Hamiltonian Cycle
Given a graph $G = (V, E)$, is there a cycle that visits every vertex exactly once?
:::

$$
\exists L \exists S\left(\begin{array}{l}
\text { linear order }(L) \\
\wedge S \text { is the successor relation of } L \\
\wedge \forall x \exists y(L(x, y) \vee L(y, x)) \\
\wedge \forall x \forall y(S(x, y) \rightarrow E(x, y))
\end{array}\right)
$$


$L$ and $S$ are binary relations.

# Chapter 1: Introduction
Example 1: $NP$ vs $\exists SO$

::: {.block}
### 3 Colorability
Given a graph $G = (V, E)$, can we color the vertices with three colors such that no two adjacent vertices have the same color?
:::

$$
\exists A \exists B \exists C\left(\begin{array}{c}
\forall x\left[\begin{array}{c}
(A(x) \wedge \neg B(x) \wedge \neg C(x)) \\
\vee(\neg A(x) \wedge B(x) \wedge \neg C(x)) \\
\vee(\neg A(x) \wedge \neg B(x) \wedge C(x))
\end{array}\right] \\
\wedge \\
\forall x, y E(x, y) \rightarrow \neg\left[\begin{array}{c}
(A(x) \wedge A(y)) \\
\vee(B(x) \wedge B(y)) \\
\vee(C(x) \wedge C(y))
\end{array}\right]
\end{array}\right)
$$

$A$, $B$, and $C$ are predicates.


# Chapter 1: Introduction
Example 2: Formal Language Theory

### Theorem
First Order Logic (FOL) is not expressive enough to express regular languages. (E.g. $(aa)^*$)

# Chapter 1: Introduction

### Fagin's Theorem
The set of all properties expressible in existential second-order logic is precisely the complexity class $NP$. That is, $NP = \exists SO$.
<!-- oldest theorem in descriptive complexity -->

# Chapter 1: Introduction
* What is Finite Model Theory
* Example 1: $NP = \exists SO$
    * Graph example 1: Reachability
    * Graph example 2: Hamiltonian Cycle
    * Graph example 3: 3 Colorability
* Example 2: Formal Language Theory
    * Example 4: Regular Languages are not $FO$ expressible

# Chapter 2: Preliminaries

::: {.block}
### Definition
A vocabulary $\sigma$ is a collection of constant symbols $(
c_1, \ldots)$, relation (or predicate), symbols $(P_1, \ldots)$ and function
symbols $(f_1, \ldots)$.
:::

For example, in a graph:

* The vertices $V$ are the constant symbols.
* The edges $E$ are the relation symbols.
* The colors $C$ are the function symbols.

Each relation and function symbol has an associated arity.

# Chapter 2: Preliminaries

### Definition
A $\sigma$-structure $\mathfrak{U}$

$$\mathfrak{U} = \langle A, \{ c^\mathfrak{U}_i \}, \{ P^\mathfrak{U}_i \}, \{ f^\mathfrak{U}_i \} \rangle$$

consists of a universe $A$ together with an interpretation of

* each constant symbol $c_i$ from $\sigma$ as an element $c^\mathfrak{U}_i \in A$
* each $k$-ary relation symbol $P_i$ from $\sigma$ as a $k$-ary relation on $A$; that is, a set $P^\mathfrak{U}_i \subseteq A^k$
* each $k$-ary function symbol $f_i$ from $\sigma$ as a function $f^\mathfrak{U}_i : A^k \rightarrow A$.



# Chapter 2: Preliminaries
* A theory $T$ is a set of sentences $\{ \Phi_i \}_i$.
* A $\sigma$-structure $\mathcal{U}$ is a model of a theory $T$ iff for every sentence $\Phi$ of $T$, the structure A is a model of $\Phi$.
* A theory $T$ is called consistent if it has a model.


# Chapter 2: Preliminaries

### Compactness Theorem
A theory $T$ is consistent if and only if every finite subset of $T$ is consistent.

### Löwenheim-Skolem Theorem
If $T$ has an infinite model, then it has a countable model.

# Chapter 1 (Revisited): Introduction
Example 1: $NP$ vs $\exists SO$

1. 3 Colorability: Given a graph $G = (V, E)$, can we color the vertices with three colors such that no two adjacent vertices have the same color?

Logic formula:
$$
\exists A \exists B \exists C\left(\begin{array}{c}
\forall x\left[\begin{array}{c}
(A(x) \wedge \neg B(x) \wedge \neg C(x)) \\
\vee(\neg A(x) \wedge B(x) \wedge \neg C(x)) \\
\vee(\neg A(x) \wedge \neg B(x) \wedge C(x))
\end{array}\right] \\
\wedge \\
\forall x, y E(x, y) \rightarrow \neg\left[\begin{array}{c}
(A(x) \wedge A(y)) \\
\vee(B(x) \wedge B(y)) \\
\vee(C(x) \wedge C(y))
\end{array}\right]
\end{array}\right)
$$

# Chapter 2: Preliminaries

Revisiting the example of 3 Colorability:

* The FOL formula $\Phi$ is a *sentence* of the theory $T$.
* The graph $G=C_5$ is a *finite model* that satisfies the theory $T$. ($(V, E) \models T$)
    * This makes $T$ consistent.


# Chapter 2: Preliminaries
* $\sigma$-structures (model)
* First Order Logic
* Queries
* Consistency: A theory $T$ is consistent if and only if it has a model.
* Compactness Theorem: A theory $T$ is consistent if and only if every finite subset of $T$ is consistent.
* Löwenheim-Skolem Theorem: If $T$ has an infinite model, then it has a countable model.
* We might want to go back to chapter 1 and flesh things out.

# Chapter 3: Ehrenfeucht-Fraïssé Games
* Finite models vs infinite models (important)
* The game itself

# Chapter 3: Ehrenfeucht-Fraïssé Games (Example)
* The two proofs (pick one)


# Chapter 11: Finite Variable Logics
* Pebble Games

# Extra 

The well known Pythagorean theorem $x^2 + y^2 = z^2$ was  proved to be invalid for other exponents. 
Meaning the next equation has no integer solutions:
$$x^n + y^n = z^n$$

Can AI, help find near misses for this equation?
