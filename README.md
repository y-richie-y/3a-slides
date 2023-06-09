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
# Chapter 1: What is Finite Model Theory?
<!-- 
# Chapter 1: Introduction
* What is Finite Model Theory
* Example 1: $NP = \exists SO$
    * Graph example 1: Reachability
    * Graph example 2: Hamiltonian Cycle
    * Graph example 3: 3 Colorability
* Example 2: Formal Language Theory
    * Example 4: Regular Languages are not $FO$ expressible -->
* Finite model theory studies the expressive power of logics on finite models.
    * Finite graphs
    * Finite strings ...
* Classical model theory, on the other hand, concentrates on infinite structures.
    * $\langle\mathbf{C}, +, \cdot\rangle$
    * $\langle\mathbf{R}, +, \cdot, <\rangle$
    * Infinite graphs ...

# Chapter 1: Example 1 ($NP$ vs $\exists SO$)
<!--
The class of problems in NP
The set of formulas in existential second-order logic

in ESO the existential quantifiers can be over
1st order relations and functions
-->

<!-- Can't express reachability in FOL -->

### Hamiltonian Cycle
Given a graph $G = (V, E)$, is there a cycle that visits every vertex exactly once?

### 3 Colorability
Given a graph $G = (V, E)$, can we color the vertices with three colors such that no two adjacent vertices have the same color?

# Chapter 1: Example 1 ($NP$ vs $\exists SO$)

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

# Chapter 1: Example 1 ($NP$ vs $\exists SO$)

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


# Chapter 1: Example 1 ($NP$ vs $\exists SO$)

### Fagin's Theorem
The set of all properties expressible in existential second-order logic is precisely the complexity class $NP$. That is, $NP = \exists SO$.
<!-- oldest theorem in descriptive complexity -->

# Chapter 1: Example 2 (Formal Language Theory)

### Theorem
First Order Logic (FOL) is not expressive enough to express regular languages. (E.g. $(aa)^*$)

# Chapter 2: Preliminaries

::: {.block}
### Definition
A vocabulary $\sigma$ is a collection of constant symbols $(
c_1, \ldots)$, relation (or predicate) symbols $(P_1, \ldots)$ and function
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

Graph example: edge symbols $E_i$ are sent to pairs of vertices $\in A^2$.

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

Goal: prove inexpressibility results for finite structures.

* General strategy: Suppose the desired property is expressible by a sentence FOL. Find two structures that agree on all FO sentences where one satisfies the property but the other does not.

* In particular: partition FO sentences into classes FO[1], FO[2],..., FO[$k$],... and for each $k$, find structures $\mathfrak{A}_k$ and $\mathfrak{B}_k$ sutch that $\mathfrak{A}_k\vDash \phi \iff \mathfrak{B}_k\vDash \phi$ for all FO[$k$] sentences $\phi$, but $\mathfrak{A}_k$ has property $\mathcal{P}$ while $\mathfrak{B}_k$ does not.

Big question 1: how can we define FO[$k$]?

Big question 2: how can we prove when structures agree on FO[$k$]?


# Chapter 3: Ehrenfeucht-Fraïssé Games

The Ehrenfeucht-Fraïssé game is a two-player sequential move game with the following components.

Players:

* Spoiler
* Duplicator

Board: two structures, e.g. $\mathfrak{A}$ and $\mathfrak{B}$

Goal:

* Spoiler wants to show that the two structures are different
* Duplicator wants to show that the two structures are the same

# Chapter 3

### Definition (Partial Isomorphism).

Let $\mathfrak{A}$, $\mathfrak{B}$ be two $\sigma$-structures, where $\sigma$ is relational, and $\vec{a}=(a_1,\dots,a_n)$ and $\vec{b}=(b_1,\dots,b_n)$ two tuples in $\mathfrak{A}$ and $\mathfrak{B}$ respectively. Then $(\vec{a},\vec{b})$ is a partial isomorphism between $\mathfrak{A}$ and $\mathfrak{B}$ when the following conditions hold.

* For every $i,j\leq n$, $a_i=a_j\iff b_i=b_j$.
* For every constant symbol $c$ from $\sigma$ and every $i\leq n$, $a_i=c^\mathfrak{A} \iff b_i=c^\mathfrak{B}$.
* For every $k$-ary relation symbol $P$ from $\sigma$ and every sequence $(i_1,\dots,i_k)$ of not necessarily distinct numbers from $[1,n]$, $(a_{i_1},\dots,a_{i_k})\in P^\mathfrak{A} \iff (b_{i_1},\dots,b_{i_k})\in P^\mathfrak{B}$.

# Chapter 3: Ehrenfeucht-Fraïssé Games

How to play:

* The players play a certain number of rounds.
* In each round, the spoiler picks a structure $\mathfrak{A}$ or $\mathfrak{B}$ and an element of that structure $a\in\mathfrak{A}$ or $b\in \mathfrak{B}$.
* The duplicator responds by picking an element from the other structure.

<!--# Chapter 3: Ehrenfeucht-Fraïssé Games-->

Winning:

* Let $\vec{a} = (a_1,\dots,a_n)$ and $\vec{b} = (b_1,\dots,b_n)$ be the moves played after $n$ rounds of an E-F Game. Also, let $\vec{c}^\mathfrak{A}$ denote $(c_1^\mathfrak{A},\dots,c_l^\mathfrak{A})$ and similarly for $\vec{c}^\mathfrak{B}$.
* $(\vec{a},\vec{b})$ is a winning position for the duplicator if $((\vec{a},\vec{c}^\mathfrak{A}),(\vec{b},\vec{c}^\mathfrak{B}))$ is a partial isomorphism between $\mathfrak{A}$ and $\mathfrak{B}$.
* When the duplicator has an $n$-round winning strategy, write $\mathfrak{A}\equiv_n\mathfrak{B}$.

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

# Chapter 3: Composition Method Proof

:::{.block}
### Lemma.
Let $L_1, L_2, a\in L_1, b\in L_2$ satisfy $L_1^{\leq a}\equiv_k L_2^{\leq b}$ and $L_1^{\geq a}\equiv_k L_2^{\geq b}$. Then $(L_1,a)\equiv_k (L_2,b)$.
:::

Proof: The duplicator just uses the winning strategy for whichever substructure the spoiler plays in. The duplicator responds to $b$ with $a$ and $a$ with $b$. This implies they can win the $k$ round game on $(L_1,a)$ and $(L_2,b)$.

# Chapter 3: Composition Method Proof (Cont.)

Use induction on $k$. Base case is trivial. For the inductive step, assume $L_1, L_2$ have length at least $2^k$ and that the spoiler plays some $a\in L_1$ (symmetric for $L_2$). We need to find $b\in L_2$ s.t. $(L_1,a)\equiv_{k-1} (L_2,b)$. 

* If length of $L_1^{\leq a} \leq 2^{k-1}$, we let $b\in L_2$ such that $L_1^{\leq a}\cong L_2^{\leq b}$ (i.e. $d(\min(L_1),a) = d(\min(L_2),b)$). We also know that the length of $L_1^{\geq a}$ and $L_2^{\geq b}$ is at least $2^{k-1}$, so by the IH, $L_1^{\geq a}\equiv_{k-1} L_2^{\geq b}$. Thus $(L_1, a)\equiv_{k-1} (L_2, b)$ by preceding lemma.
* If length of $L_1^{\geq a} \leq 2^{k-1}$, use the same strategy as above.
* Otherwise, the length of $L_1^{\leq a}$ and $L_1^{\geq a}$ are both at least $2^{k-1}$. In this case, choose $b\in L_2$ such that the lengths of $L_2^{\leq b}$ and $L_2^{\geq b}$ are at least $2^{k-1}$ (possible because length $L_2\geq 2^k$). So by the IH, $L_1^{\geq a}\equiv_{k-1} L_2^{\geq b}$ and $L_1^{\leq a}\equiv_{k-1} L_2^{\leq b}$ so $(L_1, a)\equiv_{k-1} (L_2, b)$.

So since $(L_1, a)\equiv_{k-1} (L_2, b)$ for any $a\in L_1$, we have $L_1\equiv_k L_2$ as desired.


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

* Two $\sigma$-structures $\mathfrak{A}$ and $\mathfrak{B}$ agree on a set of FO sentences $S$ if for all $\phi\in S$, $\mathfrak{A}\vDash \phi \iff \mathfrak{B}\vDash \phi$.

This answers Big Question 1!

# Chapter 3: Equivalence of E-F Games and FOL

The following Theorem and Corollary allow us to prove inexpressibility results of FO on finite structures using E-F games.

:::{.block}
### Theorem (Ehrenfeucht-Fraïssé).
Let $\mathfrak{A}$ and $\mathfrak{B}$ be two structures in a relational vocabulary. Then the following are equivalent.

* $\mathfrak{A}$ and $\mathfrak{B}$ agree on FO[$k$].
* $\mathfrak{A}\equiv_k \mathfrak{B}$.
:::

:::{.block}
### Corollary.
A property $\mathcal{P}$ of finite $\sigma$-structures in not expressible in FO if for every $k\in\mathbb{N}$, there exist two finite $\sigma$-structures, $\mathfrak{A}_k$ and $\mathfrak{B}_k$, such that

* $\mathfrak{A}_k\equiv_k \mathfrak{B}_k$, and
* $\mathfrak{A}_k$ has property $\mathcal{P}$ yet $\mathfrak{B}_k$ does not.
:::

This answers Big Question 2!

# Chapter 3: Applications of E-F Games

Let's put these results to use!

:::{.block}
### Corollary.
Even is not FO-expressible over linear orders.
:::

Proof: Let $\mathfrak{A}_k$ be a linear order of length $2^k$ and $\mathfrak{B}_k$ be a linear order of length $2^k + 1$. We already proved that $\mathfrak{A}_k\equiv_k\mathfrak{B}_k$. Since the length of $\mathfrak{A}_k$ is even and the length of $\mathfrak{B}_k$ is odd, even is not FO-expressible.

# Chapter 3: Applications of E-F Games

Graph connectivity is not FO-expressible over finite graphs.

Define an edge relation from a linear order:

* If $y = succ(succ(x))$, then $E(x,y)$.
* If $z$ is last element and $z = succ(x)$ and $y$ is the first element, then $E(x,y)$.
* If $x$ is the last element and $y$ is the successor of the first element, then $E(x,y)$.

Even length linear orders will have 2 connected components while odd length linear orders will have 1.

# Chapter 3: Applications of E-F Games

Other properties of finite graphs that can be shown to be FO-inexpressible using E-F games include:

* "Treeness",
* Acyclicity,
* Planarity,
* Hamiltonicity,
* $k$-colorability for $k\geq 2$,
* Existence of a clique of size at least $n/2$ for an $n$-node graph.


# Chapter 11: Finite Variable Logics
## Pebble Games

the spoiler and the duplicator have
a fixed set of pairs of pebbles, and each move consists of placing a pebble on
an element of a structure, or removing a pebble and placing it on another
element. Second, the game does not have to end in a finite number of rounds
(but we can still determine who wins it)

# Chapter 11: Pebble Game

Let $\mathfrak{A}, \mathfrak{B} \in \operatorname{STRUCT}[\sigma]$.
A $k$-pebble game over $\mathfrak{A}$ and $\mathfrak{B}$ is played by the spoiler and the duplicator as follows. The players have a set of pairs of pebbles $\left\{\left(p_{\mathfrak{A}}^1, p_{\mathfrak{B}}^1\right), \ldots,\left(p_{\mathfrak{A}}^k, p_{\mathfrak{B}}^k\right)\right\}$. In each move, the following happens:

<!-- - The spoiler chooses a structure, $\mathfrak{A}$ or $\mathfrak{B}$, and a number $1 \leq i \leq k$.
For the description of the other moves, we assume the spoiler has chosen $\mathfrak{A}$. The other case, when the spoiler chooses $\mathfrak{B}$, is completely symmetric. -->
- The spoiler chooses a structure, $\mathfrak{A}$ or $\mathfrak{B}$, and a number $1 \leq i \leq k$. (w.l.o.g. assume $\mathfrak{A}$ is chosen)
- The spoiler places the pebble $p_{\mathfrak{A}}^i$ on some element of $\mathfrak{A}$. If $p_{\mathfrak{A}}^i$ was already placed on $\mathfrak{A}$, this means that the spoiler either leaves it there or removes it and places it on some other element of $\mathfrak{A}$; if $p_{\mathfrak{A}}^i$ was not used, it means that the spoiler picks that pebble and places it on an element of $\mathfrak{A}$.
- The duplicator responds by placing $p_{\mathfrak{B}}^i$ on some element of $\mathfrak{B}$.

# Chapter 11: Pebble Game

We denote the game that continues for $n$ rounds by $\mathrm{PG}_k^n(\mathfrak{A}, \mathfrak{B})$, and the game that continues forever by $\mathrm{PG}_k^{\infty}(\mathfrak{A}, \mathfrak{B})$.

After each round of the game, the pebbles placed on $\mathfrak{A}$ and $\mathfrak{B}$ define a relation $F \subseteq A \times B$ : if $p_{\mathfrak{A}}^i$, for some $i \leq k$, is placed on $a \in A$ and $p_{\mathfrak{B}}^i$ is placed on $b \in B$, then the pair $(a, b)$ is in $F$.

The duplicator has a winning strategy in $\mathrm{PG}_k^n(\mathfrak{A}, \mathfrak{B})$ if he can ensure that after each round $j \leq n$, the relation $F$ defines a partial isomorphism. That is, $F$ is a graph of a partial isomorphism. In this case we write $\mathfrak{A} \equiv_{k, n}^{\infty \omega} \mathfrak{B}$.
The duplicator has a winning strategy in $\mathrm{PG}_k^{\infty}(\mathfrak{A}, \mathfrak{B})$ if he can ensure that after every round the relation $F$ defines a partial isomorphism. This is denoted by $\mathfrak{A} \equiv_k^{\infty} \mathfrak{B}$.

# Connection to Graph Isomorphism

The $k$-dimensional Weisfeiler-Leman algorithm is a powerful tool for studying the graph isomorphism problem. It is also used to describe the expressive power of graph neural networks.

# Connection to Graph Isomorphism

The $k$ Weisfeiler-Leman test takes all subsets of vertices
of size $k$ out of $n$ and assigns them a colour determined by the subgraph formed by the $k$ vertices. $k$-subgraphs that are isomorphic to each other are assigned the same colour
and grouped into a cell. Each of the
$\begin{pmatrix}n \\ k\end{pmatrix}$
subgraphs of size $k$ belong to exactly one of
$2^{\begin{pmatrix}k \\ 2\end{pmatrix}}$
classes of k-subgraphs.

# Connection to Graph Isomorphism

The $k$-dimensional Weisfeiler-Leman algorithm distinguishes two graphs if and only if the player Spoiler has a winning strategy in the __bijective__ pebble game played with $k + 1$ pairs of pebbles on the two graphs.

Bijective pebble game: the Duplicator has to provide a bijection between the elements of the two structures after the Spoiler chooses a pebble, but before the Spoiler places the pebble.
