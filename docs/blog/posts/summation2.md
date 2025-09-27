---
title : Sums over Countable Spaces
date:
  created: 2025-09-21
categories: 
    - Maths
---

## The Finite Case

Suppose I have a space $X$ with three elements, we can represent this space with the set $\{\alpha, \beta, \gamma\}$. I want to be able to talk about sums over this space. Of course, $\alpha + \beta + \gamma$ doesn't make any sense. The elements of $X$ simply serve as placeholders for the values that we want to add, in other words, we are using the "three-ness" of the space $X$ to define a sum of three values. We can do this by assigning to each element $x\in X$ a real number $r\in \mathbb{R}$, i.e. by defining a weight function $w:X\to \mathbb{R}$. The sum over the space $X$ with respect to the weight $w$ is then simply $\sum_{x\in X}w(x) = w(\alpha) + w(\beta) + w(\gamma)$.

<!-- more -->

This works fine for finite spaces, but if $X$ is countably infinite then we quickly run into some problems. For example, we can try to define the sum this way : Since $X$ is countably infinite, then there is a bijection $g:\mathbb{N}\to X$. By indexing the elements of $X$, we can definte the sum as an infinite series :

$$ \sum_{n=1}^\infty{w(g(n))} $$

However, in addition to convergence issues, it is also not entirely obvious if a different choice of $g$ (a different rearrangement of the sum) will change the evaluation of the sum[^1]. It turns out we can solve these issues by working in the space $[0,\infty]$. We can do this by setting the codomain of our weight function to the space $[0,\infty]$. 

!!! note "The Space $[0,\infty]$"

    This space is constructed by adding a point "$\infty$" to the space $[0,\infty)$. We can think of $[0,\infty]$ as a linearly ordered topological space where the order on $[0,\infty)$ is extended by setting $x\leq \infty$ for all $x\in [0,\infty]$. Furthermore, we extend addition on this space by setting $\infty + x = x+\infty = \infty$ for all $x\in [0,\infty]$. 
    
    - The order on $[0,\infty]$ is complete, i.e. any subset of $[0,\infty]$ has a supremum.
    - We can also talk about the convergence of sequences in $[0,\infty]$ via its order topology. 

Due to the monotone convergence theorem, our sum has to converge to some $x\in[0,\infty]$. Intuitively, the order of summation should also not matter if we only concern ourselves with adding non-negative terms although we will prove this rigorously later on. 

## The General Case

With all this in mind, we come up with the following "order-free" definition for the sum over a countable space $X$ by taking the supremum over all finite sub-sums :

> **Definition 1**. Let $X$ be a countable space. We define the sum over a subset $A\subseteq X$ with respect to some weight $w:X\to [0,\infty]$ with $\mu_w(A)$, where
>
> $$ \mu_w(A) := \sup\left\{\sum_{x\in F}w(x) \ \vert \ F\subseteq A, \ \text{finite }F \right\}, $$
>
> **Reminder.** Since we are working in the space $[0,\infty]$, the supremum always exists (set $\sup A := \infty$ if $A$ is unbounded), thus $\mu_w(A)$ is well-defined. If there is no confusion, we may drop the weight in the notation.

Here are some notes that may be useful :

!!! note "Note 1"

    If $A$ is finite then $\mu(A)$ reduces to the finite sum $\sum_{x\in A}w(x)$. Notice for $A=\varnothing$ we are adding nothing so that $\mu(\varnothing) = 0$.

!!! note "Note 2"

    For any $A\subseteq B$ we have $\mu(A)\leq \mu(B)$ purely because

    $$ \left\{\sum_{x\in F}w(x) \ \vert \ F\subseteq A, \ \text{finite }F \right\} \subseteq \left\{\sum_{x\in F}w(x) \ \vert \ F\subseteq B, \ \text{finite }F \right\} $$

!!! note "Note 3"

    To prove $\mu(A)\leq r$ it suffices to show that $r$ is an upper bound of $\{\sum_{x\in F}w(x) \ \vert \  F\subseteq A, \ \text{finite }F\}$, i.e. that for any finite $F\subseteq A$ we have $\sum_{x\in F}w(x) \leq r$. On the other hand, to show that $r\leq \mu(A)$ it suffices to show that there exists a finite $F\subseteq A$ such that $r\leq \sum_{x\in F}w(x)$.

## Increasing Sequences of Subsets

> **Definition 2**. Let $A \subseteq X$. We say that a sequence of sets $\{A_n\}_{n\in \mathbb{N}}$ **increases** to $A$ (denoted $A_n\nearrow A$) if the following are satisfied : 
>
> - $A_1\subseteq A_2\subseteq \cdots \subseteq A$ and 
> - $\bigcup_{n=1}^\infty A_n = A$
>
> **Note.** To prove the second condition, it suffices to show that for every $x\in A$ there exists an $N\in \mathbb{N}$ such that $x\in A_N$. 

The following lemmas allow us to reframe our arguments in terms of sequences which should prove helpful later on :

> **Lemma 1**. For any $A \subseteq X$ there exists a sequence of finite sets that increases to $A$.

??? note "Proof" 

    If $A$ is finite, then this is trivial. Suppose $A$ is countably infinite, then there exists a bijection $g:\mathbb{N}\to A$. For each $n: \mathbb{N}$ define $A_n := \{g(i) : i\leq n\}$. It is pretty clear that $A_1\subseteq A_2\subseteq \cdots \subseteq A$ and that each $A_n$ is finite.
    
    Now suppose $x\in A$, then there exists an $N\in \mathbb{N}$ such that $x = g(N)\in A_N$ by definition. Thus $A_n\nearrow A$ as needed.

> **Lemma 2**. For any $A \subseteq X$ and $A_n\nearrow A$, we have $\mu(A_n)\to \mu(A)$.

??? note "Proof"

    By Note 2 we have $\mu(A_1)\leq \mu(A_2)\leq \cdots \leq \mu(A)$, thus $\mu(A_n)$ converges to some $L\in [0,\infty]$ with $L\leq \mu(A)$ by the Monotone Convergence Theorem. Now it suffices to show that $\mu(A)\leq L$ (Note 3). Suppose $F\subseteq A$ is finite then there is an $N\in \mathbb{N}$ large enough so that $F\subseteq A_N$, thus :
  
    $$ \sum_{x\in F}w(x) \leq \mu(A_N)\leq L $$

    so we are done.

Combining these two lemmas, we get the following :

> **Theorem 1.** For any $A\subseteq X$ there exists a sequence $A_1, A_2, \ldots$ of finite sets such that $\mu(A_n)\to \mu(A)$. 

## Countable Additivity

> **Lemma 3** (Finite Additivity). Let $A_1, A_2, \cdots, A_N \subseteq X$ be a finite collection of pairwise disjoint sets, then :
>
>   $$ \mu\left(\bigcup_{n=1}^N A_n\right) = \sum_{n=1}^N \mu(A_n). $$

??? note "Proof"

    It suffices to show that for any disjoint $A,B \subseteq X$ we have $\mu(A\cup B) = \mu(A) + \mu(B)$; the rest of the argument follows inductively. Also notice that the above identity is trivial for finite $A$ and $B$.

    **Part 1 :** $\mu(A\cup B)\leq \mu(A) + \mu(B)$. 
    
    Suppose $F\subseteq A\cup B$ is finite. Now define $F_1 = F\cap A, \ F_2 = F\cap B$. Notice that $F = F_1 \cup F_2$ and that $F_1, F_2$ are disjoint. Thus,
  
    $$ \mu(F) = \mu(F_1) + \mu(F_2) \leq \mu(A) + \mu(B).$$

    In other words, we have shown that $\mu(F)\leq \mu(A) + \mu(B)$ for any finite $F\subseteq A\cup B$ which is equivalent to our goal (see note 3).

    **Part 2 :** $\mu(A) + \mu(B)\leq \mu(A\cup B)$. 
    
    For any finite $F_1\subseteq A$ and $F_2\subseteq B$, notice $F_1, F_2$ are disjoint so that

    $$ \mu(F_1) + \mu(F_2) = \mu(F_1\cup F_2) \leq \mu(A\cup B).$$

    Now we Theorem 1 : There exists a sequence $\{A_n\}_{n\in \mathbb{N}}$ such that each $A_n$ is finite and $\mu(A_n)\to \mu(A)$ (and the same for $B$). Thus, for each $n\in \mathbb{N}$, 

    $$ \mu(A_n) + \mu(B_n) \leq \mu(A\cup B).$$

    Taking the limit as $n\to \infty$ gives $\mu(A)+ \mu(B)\leq \mu(A\cup B)$ as desired.

> **Theorem 2.** (Countable Additivity). Suppose $A=\bigcup_{n=1}^\infty{A_n} \subseteq X$ and the $A_n$ are pairwise disjoint, i.e. $\{A_n\}_{n\in \mathbb{N}}$ is a partition of $A$, then
>
>   $$ \mu(A) = \sum_{n=1}^\infty \mu(A_n). $$

??? note "Proof"

    **Part 1 :** $\mu(A)\leq \sum_{n=1}^\infty \mu(A_n)$

    Suppose $F\subseteq A$ is finite then only a finite number of $A_n$'s are needed to cover $F$. Thus there is an $N\in \mathbb{N}$ large enough so that $F\subseteq \bigcup_{n=1}^N A_{n}$ and by finite additivity
  
    $$ \mu(F) \leq \mu\left( \bigcup_{n=1}^N A_{n} \right) = \sum_{n=1}^N \mu(A_{n}) \leq \sum_{n=1}^\infty \mu(A_n). $$

    **Part 2 :** $\sum_{n=1}^\infty \mu(A_n)\leq \mu(A)$

    By finite additivity, for any $N\in \mathbb{N}$

    $$ \sum_{n=1}^N \mu(A_n) = \mu\left( \bigcup_{n=1}^N A_n \right) \leq \mu(A).$$

    Taking $N\to \infty$ gives us the result we need.

## Sum Partitions

Suppose we were to use $\mu$ to define sums over the space $\mathbb{N}$, would that be equivalent to the traditional infinite sum? In other words, given some weight $w:\mathbb{N}\to [0,\infty]$, is $\mu(\mathbb{N}) = \sum_{n=1}^\infty w(n)$? The LHS is defined by a supremum over all finite sums whereas the RHS is defined by the limit of its partial sums so this is not immediately obvious, but countable additivity (Theorem 2) makes this almost trivial. 

We can partition $\mathbb{N}$ into the sets $A_1 = \{1\}, \ A_2 = \{2\}, \ \ldots$ Notice that $\mu(A_n) = w(n)$ for each $n\in \mathbb{N}$ thus by countable additivity $\mu(\mathbb{N}) = \sum_{n=1}^\infty \mu(A_n) = \sum_{n=1}^\infty w(n)$. Similarly, if $g:\mathbb{N}\to \mathbb{N}$ is a bijection, then the sets $A_n = \{g(n)\}$ form a partition of $\mathbb{N}$ so $\mu(\mathbb{N}) = \sum_{n=1}^\infty w(g(n))$. In other words, infinite sums of non-negative terms are order-invariant. 

We can also partition $\mathbb{N}$ into its odd and even parts, further partition those into the sets $O_n = \{2n-1\}, \ E_n = \{2n\}$ for $n=1,2,\ldots$ and use countable additivity :

$$ \begin{align*}
\mu(\mathbb{N}) &= \mu(\mathbb{N}_{\text{odd}}) + \mu(\mathbb{N}_{\text{even}}) \\
&= \sum_{n=1}^\infty \mu(O_n) + \sum_{n=1}^\infty \mu(E_n) \\
&= \sum_{n=1}^\infty w(2n-1) + \sum_{n=1}^\infty w(2n) 
\end{align*} $$

The point is that infinite sums (with non-negative terms) can be broken down and summed piece by piece in any order which may be helpful for simplifications.

## Tonelli's Theorem (Discrete)

The space $\mathbb{N}^2$ can be visualized as an infinite 2d matrix. A weight $w:\mathbb{N}^2\to [0,\infty]$ on this space can be visualized by setting the entry at the $n$-th row and $m$-th column of the matrix to equal $w(n,m)$. Summing over $\mathbb{N}^2$ is therefore summing over all entries of the corresponding matrix. Tonelli's Theorem states that if all entries are non-negative, then summing across all rows is equivalent to summing across all columns. More formally, we can define the subsets 

$$ R_n = \{(n,i) \ \vert \  i\in\mathbb{N}\}, \quad C_n = \{(i,n) \ \vert \ i\in\mathbb{N}\} $$

to specify the rows and columns of the matrix respectively. Thus Tonelli's Theorem states that :

$$ \sum_{n=1}^\infty \mu(R_n) = \sum_{n=1}^\infty \mu(C_n) $$

which is trivial by countable additivity. Note that $\mu(R_n) = \sum_{i=1}^\infty w(n,i)$ and $\mu(C_n) = \sum_{i=1}^\infty w(i,n)$, thus we can restate the above as a double sum :

$$ \begin{align*}
\sum_{n=1}^\infty \sum_{i=1}^\infty w(n,i) &= \sum_{n=1}^\infty \sum_{i=1}^\infty w(i,n) \\
&= \sum_{i=1}^\infty \sum_{n=1}^\infty w(n,i), \quad \quad \text{(relabel/swap index)}
\end{align*} $$








[^1]: In fact the choice of $g$ does matter, see the [Riemann Rearrangement Theorem](https://en.wikipedia.org/wiki/Riemann_series_theorem)