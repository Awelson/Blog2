---
title : About Sequences..
date:
  created: 2025-09-21
categories: 
    - Maths
---

## Introduction

A sequence in some space $X$ is usually represented by some function $a:\mathbb{N}\to X$ so that the first term of the sequence is $a(1)$, the second is $a(2)$ and so on. However, we usually write $a_n$ in place of $a(n)$ for aesthethic reasons.

<!-- more -->

Given a sequence $a$ of points in $X$, an interesting question to ask is whether or not this sequence converges to some $L\in X$. In order for this question to make sense there has to be some notion of distance on the space $X$, which we can do by specifying a [metric](https://en.wikipedia.org/wiki/Metric_space) (or more generally a [topology](https://en.wikipedia.org/wiki/Topological_space)) on $X$. 

Very briefly, a metric on $X$ is a function $d:X\times X\to \mathbb{R}$ that can be used as some sort of "ruler" on $X$; for any $x,y\in X$ the real number $d(x,y)$ represents how far away these two points are from each other, the smaller $d(x,y)$ is the closer $x$ and $y$ are and vice-versa. 

!!! warning 

    Of course, a metric has to "make sense". For example, we cannot have $d(x,x)=2$, or $d(x,y)<0$, and so on. There is a list of properties that a function $d:X\times X\to \mathbb{R}$ has to satisfy in order for it to "make sense" to be used as a metric. For example $d(x,y):= |x-y|$ is an example of a function that makes sense to be used as a metric on the space $\mathbb{R}$. I won't get into all of the details here since it suffices to just have an intuitive idea; you can of course look into it at your own time.

## Eventual Behavior of a Sequence

Intuitively speaking, convergence is an *eventual behavior* of a sequence. For example, if $a\to L$ then any modification of $a$ that does not alter its eventual behavior (for example, removing the first 100 terms) will not affect its convergence. To be more specific, a sequence $a$ *eventually* satisfies some property $P$ if there is some index $N\in \mathbb{N}$ such that $P$ is satisfied by $a_N, a_{N+1}, a_{N+2}, \ldots$ 

!!! example

    Let $P$ be the property "is equal to 1". Then the sequence 

    $$ 5,4,3,2,1,1,1,1,\ldots $$

    eventually satisfies $P$ since $a_n = 1$ for all $n\geq 5$.

Instead of talking about properties, we can talk about subsets. To say that a sequence $a$ of points in $\mathbb{N}$ is "eventually equal to 1" or "is eventually even" amounts to saying that $a$ will eventually be contained in the subsets $\{1\}$ or $\{2n \ \vert \ n\in \mathbb{N}\}$ respectively. In other words, there is a 1-to-1 correspondence between a property on some space $X$ and its subsets. Thus, we may simplify things by declaring that the only property we should concern ourselves with is that of containment in some subset :

> **Definition 1.** A sequence $a$ on some space $X$ is said to be eventually contained in some subset $A\subseteq X$ if there exists an $N\in \mathbb{N}$ such that $a_n\in A$ for all $n\geq N$.

If we can find some $N\in \mathbb{N}$ for which $a_n\in A$ for all $n\geq N$, then the number of indices $m$ for which $a_m \notin A$ cannot be greater than $N-1$. In other words there are only a finite number of, we shall say "bad" indices. On the other hand, if there are only a finite number of bad indices, then there has to be the largest "bad" index, which we'll call $M$. This implies that $a_n\in A$ whenever $n\geq M+1$, i.e. we have shown that $a$ is eventually contained in $A$. In conclusion, the "eventual behavior" of a sequence can be reframed via the finiteness of its set of bad indices.

Recall that a sequence is really just a function $a:\mathbb{N}\to X$. Thus, the set of bad indices can be expressed in terms of the inverse image : $a^{-1}[A^c]$. Similarly, the set of "good indices" can be represented by $a^{-1}[A]$. Clearly, taking the complement of the good indices gives us the bad indices (and vice-versa). This gives us the following identity :

$$ a^{-1}[A]^c = a^{-1}[A^c] $$

In other words, the inverse image of a complement is a complement of the inverse image, which is true in general. We will use this concept to define yet another way to reframe "eventual behavior" : Instead of checking to see if the set of bad indices is finite, we can try to check to see if the set of good indices is "large enough". 

Notice that having an infinite number of elements is not a sufficient condition for a set to be "large enough". For example, if the good indices are : $2,4,6,8,\ldots$ then this implies the existence of an infinite number of bad indices, namely $1,3,5,7,\ldots$ Thus, we need a stronger condition for "large enough". Consider the following :

> **Definition 2**. Let $A$ be some subset of a space $X$. We say that $A$ is cofinite if $A^c := X\setminus A$ is finite. Let $Fr$ be the collection of all cofinite subsets of $\mathbb{N}$, we call $Fr$ the [Fréchet filter](https://en.wikipedia.org/wiki/Fr%C3%A9chet_filter).

By construction, cofinite sets are indeed "large enough" for our needs, i.e. it becomes trivial that : the set of bad indices is finite iff the set of good indices is cofinite (is contained in the Fréchet filter). Thus, whenever I say that a sequence $a$ is *eventually* contained in $A$, it can mean either of the following conditions :

- There exists an $N\in \mathbb{N}$ such that $a_n\in A$ for $n\geq N$
- The set of bad indices is finite : $a^{-1}[A^c]$ is finite
- The set of good indices is cofinite : $a^{-1}[A]\in Fr$

Afterall, we have shown that all three are equivalent.  

### Convergence as an Eventual Behavior

> **Definition 3**. For any $\epsilon>0$ and $L\in X$ we define $B_\epsilon(L):=\{x\in X \ \vert \ d(L,x)<\epsilon\}$. This can be thought of as the collection of points that are close to $L$. Thinking of $\epsilon>0$ as a parameter, we can control exactly how close the points in $B_\epsilon(L)$ are to $L$.  

!!! example

    In the space $\mathbb{R}$ with the metric $d(x,y):=|x-y|$, the set $B_1(0)$ is exactly the open interval $(-1,1)$.

Fix some $L\in X$. It makes sense to say that a sequence $a\to L$ if it is eventually contained in $B_\epsilon(L)$ where $\epsilon>0$ can be controlled to specify the desired level of "closeness". For example, to say that $a$ is eventually contained in $B_1(L)$ means that the terms of $a$ will eventually be at a distance of at most 1 away from $L$. With this in mind, we come up with the following definition :

> **Definition 4**. A sequence $a$ on some metric space $X$ is said to converge to some $L\in X$ if for any $\epsilon>0$, $a$ is eventually contained in $B_\epsilon(L)$

!!! question "Exercise 1"

    Let $a$ be a sequence in $X$, $A$ be a subset of $X$ and $f:\mathbb{N}\to \mathbb{N}$ be an injection. Show that if $a$ is eventually contained in $A$, then the sequence $a\circ f$ is also eventually contained in $A$. By extension, this means that whenever $a\to L$ we also have $a\circ f \to L$. I recommend using the finiteness of the bad indices for this proof.

    ??? note "Answer"

        A key lemma which we won't prove here : 
        
        <div align="center"> For any injection $f:X\to Y$ and $A\subseteq Y$ we have $|f^{-1}[A]| \leq |A|$ </div>

        Now for the actual proof : Our goal is to show that $[a\circ f]^{-1}[A^c]$ is finite. Let $B := [a\circ f]^{-1}[A^c]$. Notice that 
        
        $$B = f^{-1}[a^{-1}[A^c]]$$

        By definition, the set $a^{-1}[A^c]$ is finite. By our lemma, $B$ has to be finite as well so we are done. 


<!-- The alternative characterization is more appealing to me because it makes some results super obvious. For example, given a sequence $a_n$ that is almost always contained in $A$, taking a subsequence or rearranging the terms of $a_n$ does not increase the number of bad indices, hence the new sequence is also almost always contained in $A$. As a direct consequence, if $a_n\to L$ then any subsequence or rearrangement of $a_n$ should also retain this behavior and converge to $L$ as well. -->

## Pushforward

This section builds up the theory needed to generalize the exercise above.

> **Definition 5**. A function $f:\mathbb{N}\to\mathbb{N}$ is said to be a pushforward if 
>
> $$\forall A\subseteq \mathbb{N}, \ A\in Fr \Rightarrow f^{-1}[A]\in Fr \tag{1}$$

!!! note

    For those that are familiar with topology, this looks awfully similar to the definition of a [continuous function](https://en.wikipedia.org/wiki/Continuous_function#Continuous_functions_between_topological_spaces). In fact, the definitions match when we consider the space $\mathbb{N}$ with the [cofinite topology](https://en.wikipedia.org/wiki/Cofiniteness#Cofinite_topology). Alas I am not knowledgeable enough to quote on why this connection exists.

In other words, a pushforward is a function whose inverse image preserves the largeness (co-finiteness) of a subset of $\mathbb{N}$. For example, the identity function is a trivial example of a pushforward.

Let $a:\mathbb{N}\to X$ be a sequence and $f:\mathbb{N}\to\mathbb{N}$ be a pushforward, then we can define a new sequence by composition : $a\circ f$. Here is a nice theorem about sequences constructed in such a manner :

> **Theorem 2**. Let $a:\mathbb{N}\to X$ be a sequence and $f:\mathbb{N}\to \mathbb{N}$ be a pushforward. If $a$ is eventually contained in some subset $A\subseteq X$ then so will $a\circ f$. By extension, whenever $a\to L$ we must also have $a\circ f \to L$.

??? note "Proof"

    What we want to show is that $a^{-1}[A]\in Fr$ implies $[a\circ f]^{-1}[A]\in Fr$. First, assume that $a^{-1}[A]\in Fr$. Now notice that $[a\circ f]^{-1}[A] = f^{-1}[a^{-1}[A]]$ and combine this with our assumption and the fact that $f$ is a pushforward.

I chose the name "pushforward" because the eventual behavior of $a$ gets ***pushed forward*** into the new sequence $a\circ f$. Another characterization of pushforwards can be obtained by noticing that the condition $(1)$ is equivalent to :

<div align="center"> $\forall \ A\subseteq \mathbb{N}$, $ \ A$ is finite $\quad \Longrightarrow \quad$ $f^{-1}[A]$ is finite <span style="float:right;">(2)</span></div>

Proving this is not too hard once you recall that for any $f:X\to Y$ and $A\subseteq Y$ we have $(f^{-1}[A])^c =  f^{-1}[A^c]$. Another equivalent condition is :

<div align="center"> $\forall m\in \mathbb{N}$, $ \ f^{-1}[\{m\}]$ is finite <span style="float:right;">(3)</span></div>

The relevant hint here is that inverse images distribute under unions : $f^{-1}[A\cup B] = f^{-1}[A] \cup f^{-1}[B]$. Finally, we have another equivalent condition :

<div align="center"> The sequence $f(n)$ diverges to $\infty$ <span style="float:right;">(4)</span></div>

To prove this, I would suggest using the contrapositive, i.e. to show that $\neg(3)\to \neg(4)$ and that $\neg(4)\to \neg(3)$, but I will leave it up to you to fill in the details.

!!! example

    We now know (by Exercise 1) that any injection $f:\mathbb{N}\to \mathbb{N}$ is also a pushforward. By definition, if $b$ is a subsequence of $a$ then $b = a\circ f$ for some strictly increasing $f:\mathbb{N}\to \mathbb{N}$. Clearly $f$ is injective and hence a pushforward. Thus we may conclude that whenever $a\to L$ we also have $b = a\circ f \to L$. We may also use the same argument to show that rearrangements of $a$ preserves the original limit (if it exists).

## Pullback

We now turn our attention to the dual concept : pullbacks.

> **Definition 7**. A function $f:\mathbb{N}\to \mathbb{N}$ is said to be a pullback if
>
> $$\forall A\subseteq \mathbb{N}, \ f^{-1}[A] \in Fr \Longrightarrow A\in Fr \tag{5}$$

Naturally, we have the corresponding theorem for "pullback sequences"

> **Theorem 3**. Let $a:\mathbb{N}\to X$ be a sequence and $f:\mathbb{N}\to \mathbb{N}$ be a pullback. If $a\circ f$ is eventually contained in some subset $A\subseteq X$ then so will $a$. By extension, whenever $a\circ f\to L$ we must also have $a \to L$.

The proof is similar and follows the same logic. An easy way to check if $f$ is a pullback is to check if its image is cofinite :

> **Theorem 4**. A function $f:\mathbb{N}\to \mathbb{N}$ is a pullback iff $Im(f)\in Fr$.

??? note "Proof"

    We start with the forward direction. Setting $A:=Im(f)$ in $(5)$ we notice that it suffices to show that $f^{-1}[Im(f)]$ is cofinite. However, notice that
    
    $$ f^{-1}[Im(f)] := \{x\in \mathbb{N} \ \vert \ f(x)\in Im(f)\} = \mathbb{N}$$

    which is obviously cofinite. For the reverse direction, let $A\subseteq \mathbb{N}$ be arbitrary. We make the assumptions : $Im(f)\in Fr$ and $f^{-1}[A]\in Fr$. Our goal is to show that $A\in Fr$, i.e. that $A^c$ is finite. First notice that $A^c$ can be decomposed into two disjoint parts based on whether or not its elements are in $Im(f)$ : 
    
    $$ A^c = \underbrace{\left(A^c \cap Im(F)\right)}_{\text{Part 1}} \cup \underbrace{\left(A^c \setminus Im(F)\right)}_{\text{Part 2}}$$

    Thus, it suffices to show that each part is finite. For part 2, notice that $A^c \setminus Im(F) = A^c \cap Im(f)^c\subseteq Im(f)^c$ which is finite by assumption so we are done. For Part 1 the following identities will prove useful :

    > For any $f:X\to Y$ and any $A\subseteq Y$ :
    >
    > $$A \cap Im(f) = f[f^{-1}[A]], \quad \quad f^{-1}[A^c] = f^{-1}[A]^c$$

    Now notice :

    $$ A^c \cap Im(F) = f[f^{-1}[A^c]] = f[f^{-1}[A]^c] $$
    
    Recall that $f^{-1}[A]^c$ is finite by assumption, thus Part 1 is the image of a finite set. The image of a finite set has still to be finite so we are done.

!!! example

    Let $f(n) := n+100$. Then $f$ is a pullback since $Im(f)\in Fr$. Suppose you were asked to show that $(a_1, a_2, \ldots)$ converges to $L$, then you could (if for some reason it is easier) prove that $(a_{101}, a_{102},\ldots)\to L$ instead, and ***pull*** that property ***back*** into the original sequence.

## Appendix

### Stich Sequences

Say we are given three sequences $a,b,c$ of points in some space $X$. We can *stitch* these sequences together to create a new sequence $\times(a,b,c)$ of points in $X$ defined by :

$$ \times(a,b,c) := a_1, b_1, c_1, a_2, b_2, c_2, a_3, \ldots $$

Of course we can *stitch* together any finite number of sequences together, as long as they map to the same space of course. 

!!! question "Exercise 2"

    If each individual sequence is eventually contained in some subset $A\subseteq X$ then would the stitched sequence also be eventually contained in $A$? How about vice-versa? Try to figure this out on your own before looking at the answer :

    ??? note "Answer"

        The reverse direction is easy to prove since we can take a subsequence of the stitched sequence to reconstruct any of its original components. We can then do a pushforward to transfer this property into each of the component sequences. 

        For the forward direction, we can notice that the number of bad indices of the stitched sequence can be obtained by summing up the bad indices of each component sequence. By assumption, each component has a finite number of bad indices and since there are only finitely many components the stitched sequence should also have a finite number of bad indices.

Here is a cool example of using stitch sequences in practice :

> **Theorem 5**. Let $f_1, f_2,\ldots f_k : \mathbb{N}\to \mathbb{N}$ be a finite collection of functions such that $\bigcup_{i=1}^k Im(f_i)\in Fr$. Suppose we have a sequence $a:\mathbb{N}\to X$. For any $A\subseteq X$, if each $a\circ f_i$ is eventually contained in $A$, then so will $a$. By extension, if each $a\circ f_i \to L$ then it is also the case that $a\to L$. 

??? note "Proof"

    Consider the stitched sequence :

    $$ s := \times(a\circ f_1, a\circ f_2, \ldots, a\circ f_k) $$

    We know that $s$ is eventually contained in $A$. It should also be clear that there is a function $F:\mathbb{N}\to \mathbb{N}$ such that $s = a\circ F$. Thus, to prove our goal it suffices to show that $F$ is a pullback. Notice that $Im(F) = \bigcup_{i=1}^k Im(f_i)$. By assumption $Im(F)\in Fr$, thus by Theorem 4 $F$ is a pullback.

### A Note on Divergence

If there is no point $L\in X$ for which $a\to L$ then we say that $a$ is divergent. In the space $\mathbb{R}$, there are three ways in which a sequence can diverge : either $a\to \infty$, $a\to -\infty$, or $a$ oscillates around. Just like how convergence can be viewed as an eventual behavior, divergence to $\infty$ or $-\infty$ can be viewed as an eventual behavior as well :

<div style="display: flex; justify-content: space-between;">
  <div> $a\to \infty$ </div>
  <div style="margin-left: auto; margin-right: auto;"> $ \ \ $ is equivalent to </div>
  <div style="white-space: nowrap;"> $\forall M>0, \ $ $a$ is eventually in $\{x\in \mathbb{R} \ \vert \ x\geq M\}$ </div>
</div>

<div style="display: flex; justify-content: space-between;">
  <div> $a\to -\infty$ </div>
  <div style="margin-left: auto; margin-right: auto;"> is equivalent to </div>
  <div style="white-space: nowrap;"> $\forall M<0, \ $ $a$ is eventually in $\{x\in \mathbb{R} \ \vert \ x\leq M\}$ </div>
</div>