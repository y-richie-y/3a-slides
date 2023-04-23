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

::: {.block}
### Definition
A $\sigma$-structure $\mathfrak{U}$

$$\mathfrak{U} = \langle A, \{ c^\mathfrak{U}_i \}, \{ P^\mathfrak{U}_i \}, \{ f^\mathfrak{U}_i \} \rangle$$

consists of a universe $A$ **together with an interpretation** of

* each constant symbol $c_i$ from $\sigma$ as an element $c^\mathfrak{U}_i \in A$
* each $k$-ary relation symbol $P_i$ from $\sigma$ as a $k$-ary relation on $A$; that is, a set $P^\mathfrak{U}_i \subseteq A^k$
* each $k$-ary function symbol $f_i$ from $\sigma$ as a function $f^\mathfrak{U}_i : A^k \rightarrow A$.
:::

Graph example: the edge symbols would get sent to pairs of vertices $\in A^2$.

<!-- So the model and the theory share a common vocabulary?
No. The interpretation maps this. -->


# Chapter 2: Preliminaries

Defining $t^\mathfrak{U}(\overrightarrow{a})$:

* $c$ is a constant symbol
    * $c \mapsto c^\mathfrak{U}$
* $x_i$ is a variable
    * $x_i \mapsto a_i$
* $f$ is a function symbol
    * $f(t_1, \ldots, t_k) \mapsto f^\mathfrak{U}(t_1^\mathfrak{U}(\overrightarrow{a}), \ldots, t_k^\mathfrak{U}(\overrightarrow{a}))$
* $P$ is a relation symbol
    * If $\phi \equiv  P(t_1, \ldots, t_k)$, then $\mathfrak{U} \models \phi(\overrightarrow{a}) \Leftrightarrow P(t_1, \ldots, t_k) \in P^\mathfrak{U}$


# Chapter 2: Preliminaries

Defining $\models$:

- If $\varphi \equiv\left(t_1=t_2\right)$, then $\mathfrak{A} \models \varphi(\vec{a})$ iff $t_1^{\mathfrak{A}}(\vec{a})=t_2^{\mathfrak{A}}(\vec{a})$.
- If $\varphi \equiv P\left(t_1, \ldots, t_k\right)$, then $\mathfrak{A} \models \varphi(\vec{a})$ iff $\left(t_1^{\mathfrak{A}}(\vec{a}), \ldots, t_k^{\mathfrak{A}}(\vec{a})\right) \in P^{\mathfrak{A}}$.
- $\mathfrak{A} \models \neg \varphi(\vec{a})$ iff $\mathfrak{A} \models \varphi(\vec{a})$ does not hold.
- $\mathfrak{A} \models \varphi_1(\vec{a}) \wedge \varphi_2(\vec{a})$ iff $\mathfrak{A} \models \varphi_1(\vec{a})$ and $\mathfrak{A} \models \varphi_2(\vec{a})$.
- $\mathfrak{A} \models \varphi_1(\vec{a}) \vee \varphi_2(\vec{a})$ iff $\mathfrak{A} \models \varphi_1(\vec{a})$ or $\mathfrak{A} \models \varphi_2(\vec{a})$.
- If $\psi(\vec{x}) \equiv \exists y \varphi(y, \vec{x})$, then $\mathfrak{A} \models \psi(\vec{a})$ iff $\mathfrak{A} \models \varphi\left(a^{\prime}, \vec{a}\right)$ for some $a^{\prime} \in A$.
- If $\psi(\vec{x}) \equiv \forall y \varphi(y, \vec{x})$, then $\mathfrak{A} \models \psi(\vec{a})$ iff $\mathfrak{A} \models \varphi\left(a^{\prime}, \vec{a}\right)$ for all $a^{\prime} \in A$.

# Chapter 2: Preliminaries

### Definition
An m-ary query, $m \geq 0$, on $\sigma$-structures, is a mapping $Q$ that associates with each structure $\mathfrak{A}$ a subset of $A^m$, such that $Q$ is closed under isomorphism: if $\mathfrak{A} \cong \mathfrak{B}$ via isomorphism $h: A \rightarrow B$, then $Q(\mathfrak{B})=h(Q(\mathfrak{A}))$

We say that $Q$ is definable in a logic $\mathcal{L}$ if there is a formula $\varphi\left(x_1, \ldots, x_m\right)$ of $\mathcal{L}$ in vocabulary $\sigma$ such that for every $\mathfrak{A}$,
$$
Q(\mathfrak{A})=\left\{\left(a_1, \ldots, a_m\right) \in A^m \mid \mathfrak{A} \models \varphi\left(a_1, \ldots, a_m\right)\right\} .
$$
If $Q$ is definable by $\varphi$, we shall also write $\varphi(\mathfrak{A})$ instead of $Q(\mathfrak{A})$. Furthermore, for a formula $\varphi(\vec{x}, \vec{y})$, we write $\varphi(\mathfrak{A}, \vec{b})$ for $\left\{\vec{a} \in A^{|\vec{a}|} \mid \mathfrak{A} \models \varphi(\vec{a}, \vec{b})\right\}$.

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

# Chapter 3: Ehrenfeucht-Fraïssé Games (Motivation)

Traditional model theoretic techniques (compactness, Lowenheim-Skolem) are not applicable to finite models.

:::{.block}
### Proposition
Connectivity of arbitrary graphs is not FO-definable.
:::

<!--Proof: Assume FO-sentence $\phi$ defines connectivity over a vocabulary $\sigma=\{E\}$. Expand $\sigma$ with two constant symbols $c_1$ and $c_2$. -->

Proof Sketch: Assume FO-sentence $\phi$ defines graph connectivity. Pick two vertices and construct a family of sentences $\psi_n$ expressing that no path between them of length $n+1$ exists for all $n$. Make a theory which contains $\phi$ and all the $\psi_n$'s. Use compactness to show that this theory is consistent. This plainly derives a contradiction.

* This proof leaves open the possibility that connectivity is FO-definable over finite graphs!

# Chapter 3: Ehrenfeucht-Fraïssé Games (Motivation cont.)

:::{.block}
### Proposition
Compactness fails over finite models, i.e., there is a theory $T$ such that

* $T$ has no finite models, and
* every finite subset of $T$ has a finite model.
:::
Proof: Assume $\sigma=\{\emptyset\}$ and define
$$
\lambda_n \equiv \exists x_1\dots \exists x_n \bigwedge\limits_{i\neq j} \neg(x_i=x_j).
$$
Let $T=\{\lambda_n \mid n\geq 0\}$. $T$ has no finite model, but for all finite $\{\lambda_{n_1},\dots,\lambda_{n_k}\}\subset T$, any set $S$ with $|S|>\max\{n_1,\dots,n_k\}$ is a model.

* Need a more tailored way to prove inexpressibility results for finite structures!


# Chapter 3: Ehrenfeucht-Fraïssé Games

The Ehrenfeucht-Fraïssé game is a two-player sequential move game with the following components.

Players:

* Spoiler
* Duplicator

Board: two structures, e.g. $\mathcal{A}$ and $\mathcal{B}$

Goal:

* Spoiler wants to show that the two structures are different
* Duplicator wants to show that the two structures are the same

# Chapter 3

### Definition (Partial Isomorphism).

Let $\mathcal{A}$, $\mathcal{B}$ be two $\sigma$-structures, where $\sigma$ is relational, and $\vec{a}=(a_1,\dots,a_n)$ and $\vec{b}=(b_1,\dots,b_n)$ two tuples in $\mathcal{A}$ and $\mathcal{B}$ respectively. Then $(\vec{a},\vec{b})$ is a partial isomorphism between $\mathcal{A}$ and $\mathcal{B}$ when the following conditions hold.

* For every $i,j\leq n$, $a_i=a_j\iff b_i=b_j$.
* For every constant symbol $c$ from $\sigma$ and every $i\leq n$, $a_i=c^\mathcal{A} \iff b_i=c^\mathcal{B}$.
* For every $k$-ary relation symbol $P$ from $\sigma$ and every sequence $(i_1,\dots,i_k)$ of not necessarily distinct numbers from $[1,n]$, $(a_{i_1},\dots,a_{i_k})\in P^\mathcal{A} \iff (b_{i_1},\dots,b_{i_k})\in P^\mathcal{B}$.

# Chapter 3: Ehrenfeucht-Fraïssé Games

How to play:

* The players play a certain number of rounds.
* In each round, the spoiler picks a structure $\mathcal{A}$ or $\mathcal{B}$ and an element of that structure $a\in\mathcal{A}$ or $b\in \mathcal{B}$.
* The duplicator responds by picking an element from the other structure.

<!--# Chapter 3: Ehrenfeucht-Fraïssé Games-->

Winning:

* Let $\vec{a} = (a_1,\dots,a_n)$ and $\vec{b} = (b_1,\dots,b_n)$ be the moves played after $n$ rounds of an E-F Game. Also, let $\vec{c}^\mathcal{A}$ denote $(c_1^\mathcal{A},\dots,c_l^\mathcal{A})$ and similarly for $\vec{c}^\mathcal{B}$.
* $(\vec{a},\vec{b})$ is a winning position for the duplicator if $((\vec{a},\vec{c}^\mathcal{A}),(\vec{b},\vec{c}^\mathcal{B}))$ is a partial isomorphism between $\mathcal{A}$ and $\mathcal{B}$.
* When the duplicator has an $n$-round winning strategy, write $\mathcal{A}\equiv_n\mathcal{B}$.

<!-- Why does winning depend on the constant symbols?-->

# Chapter 3: Ehrenfeucht-Fraïssé Games (Examples)

* When $\sigma$ is empty, a $\sigma$-structure is just a set. When $|A|,|B|\geq n$, $A\equiv_n B$.
* After $i$ rounds, the game state is $(a_1,\dots,a_i),(b_1,\dots,b_i)$. If the spoiler picks $a_{i+1}\in A$ s.t. $a_{i+1} = a_j$ for some $j \leq i$, the duplicator plays $b_j$. Otherwise, the duplicator plays any element in $B-\{b_1,\dots,b_i\}$ which is guaranteed to exist because $|B|\geq n$.

# Chapter 3: Ehrenfeucht-Fraïssé Games (Examples)

* When $\sigma$ contains a single relation symbol $<$, we can interpret this relation as a linear order to get structures of the form $L=\langle \{a_1,\dots,a_m\},<\rangle$. We want to know when $L_1\equiv_n L_2$ for $m\geq n$.
* Easy to see that this doesn't hold in general.

:::{.block}
### Theorem.

Let $k>0$, and let $L_1, L_2$ be linear orders of length at least $2^k$. Then $L_1\equiv_k L_2$.
:::

* Proof technique 1: prove by induction with a stronger IH than just partial isomorphism.
* Proof technique 2: Use the \emph{composition method}, i.e., prove results for simpler games before composing to achieve desired result.

# Chapter 3: Equivalence of E-F Games and FOL

:::{.block}
### Definition (Quantifier rank). 
The quantifier rank of a formula qr($\varphi$) is its depth of quantifier nesting. We define this inductively as follows.

* If $\varphi$ is atomic, then $\text{qr}(\varphi) = 0$.
* $\text{qr}(\varphi_1\lor \varphi_2) = \text{qr}(\varphi_1 \land \varphi_2) = \max(\text{qr}(\varphi_1),\text{qr}(\varphi_2))$.
* $\text{qr}(\neg \varphi) = \text{qr}(\varphi)$.
* $\text{qr}(\exists x \varphi) = \text{qr}(\forall x \varphi) = \text{qr}(\varphi)+1$.
:::

* FO[$k$] denotes the set of all FO formulae up to quantifier rank $k$.

* Two $\sigma$-structures $\mathcal{A}$ and $\mathcal{B}$ agree on a set of FO sentences $S$ if for all $\phi\in S$, $\mathcal{A}\vDash \phi \iff \mathcal{B}\vDash \phi$.

# Chapter 3: Equivalence of E-F Games and FOL

The following Theorem and Corollary allow us to prove inexpressibility results of FO on finite structures using E-F games.

:::{.block}
### Theorem (Ehrenfeucht-Fraïssé).
Let $\mathcal{A}$ and $\mathcal{B}$ be two structures in a relational vocabulary. Then the following are equivalent.

* $\mathcal{A}$ and $\mathcal{B}$ agree on FO[$k$].
* $\mathcal{A}\equiv_k \mathcal{B}$.
:::

:::{.block}
### Corollary.
A property $\mathcal{P}$ of finite $\sigma$-structures in not expressible in FO if for every $k\in\mathbb{N}$, there exist two finite $\sigma$-structures, $\mathcal{A}_k$ and $\mathcal{B}_k$, such that

* $\mathcal{A}_k\equiv_k \mathcal{B}_k$, and
* $\mathcal{A}_k$ has property $\mathcal{P}$ yet $\mathcal{B}_k$ does not.
:::





# Chapter 11: Finite Variable Logics
* Pebble Games

the spoiler and the duplicator have
a fixed set of pairs of pebbles, and each move consists of placing a pebble on
an element of a structure, or removing a pebble and placing it on another
element. Second, the game does not have to end in a finite number of rounds
(but we can still determine who wins it).

Why is the game part important? (e.g. taking turns moving the pebbles / extending homomorphisms)

# Extra 

The well known Pythagorean theorem $x^2 + y^2 = z^2$ was  proved to be invalid for other exponents. 
Meaning the next equation has no integer solutions:
$$x^n + y^n = z^n$$

Can AI, help find near misses for this equation?
