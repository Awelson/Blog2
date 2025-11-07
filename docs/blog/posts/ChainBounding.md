---
title : Chain Bounding
date:
  created: 2025-10-13
categories: 
    - Maths
---

This will basically be an annotated copy of some of the relevant sections in Guillermo and Pedro's [paper on chain bounding](https://arxiv.org/pdf/2404.11638) in ArXiv. Along the way, I will be filling in some gaps in their proofs/explanations. Whenever I do this, my own words will be placed in an info box.

<!-- more -->

## The greatest good chain

We introduce some notation. Let $P$ be a poset and $C\subseteq P$; we say that $s\in P$ is a *strict upper bound* of $C$  if $\forall c\in C,\ c<s$. Furthermore, if $S\subseteq C$, we say that $S$ is an *initial segment* of $C$ ($S\sqsubseteq C$) if for all $x\in C$, $x\leq y \in S$ implies $x\in S$. We will usually omit the word "initial" and simply say "$S$ is a segment of $C$". The strict version of the segment relation is denoted by $S\sqsubset C$, that is, $S\sqsubseteq C$ and $S\neq C$. Finally, $\mathcal{P}(X)$ denotes the powerset of the set $X$.

??? note "Definition (Chain)"

    The authors perhaps forgot to include the definition of a chain? A subset $C\subseteq P$ is said to be a *chain* if for all $x,y\in C$ : either $x\leq y$ or $y\leq x$. Another way to state this is that every pair of elements from $C$ has to be *comparable*. I will also add that any subset of a chain is itself a chain. This is simple enough to not warrant proving, but important enough to state.

??? note "Definition (Segment)"

    I will add some points to the definition of a segment. To be more explicit : Let $C\subseteq P$, then a subset $S\subseteq C$ is said to be a segment of $C$ (denoted $S\sqsubseteq C$) if 
    
    $$\forall x\in C, \forall y\in S, \ x\leq y \Rightarrow x\in S \tag{1}$$

    Note the precondition that $S\subseteq C$. What we really mean when we say that $S\sqsubseteq C$ are two things : that both $S\subseteq C$ and (1) are satisfied. Similarly, $S\sqsubset C$ means : $S\subset C$ and (1), or alternatively : both $S\sqsubseteq C$ and $S\neq C$ hold.

> **Definition 1.** Let $g: \mathcal{P}(P) \to \mathcal{P}(P)$ be given. We say that a chain $C\subseteq P$ is *good for* $g$ if for all $S\sqsubset C$ we have $S\sqsubset g(S) \sqsubseteq C$. When understood from the context, we omit “for $g$”. 

We have the following key result :

> **Lemma 2.** (Comparability) Let $P$ be a poset and $g: \mathcal{P}(P) \to \mathcal{P}(P)$. If $C_1$ and $C_2$ are good chains, one is a segment of the other.

*Proof.* Let $\mathcal{S}$ be the family of mutual segments of both $C_1$ and $C_2$. Hence $\bigcup \mathcal{S}$ is also a mutual segment. If $\bigcup \mathcal{S}$ is different from both $C_1$ and $C_2$, then $g(\bigcup \mathcal{S})$ should be a mutual segment since both are good; but this contradicts the fact that $g(\bigcup \mathcal{S})\not\subseteq\bigcup \mathcal{S}$.

??? note "Prepwork (Lemma 2.1)"

    > **Lemma 2.1.** Let $C\subseteq P$ and $F$ be some collection of segments of $C$, that is to say for each $S\in F, S\sqsubseteq C$. Then $\bigcup F \sqsubseteq C$.

    *Proof.* First, we prove that $\bigcup F \subseteq C$. Let $z\in \bigcup F$, then $z\in S$ for some $S\in F$. By definition, $S\sqsubseteq C$, thus $z\in S\subseteq C$ as needed. Next, we shall prove : $\forall x\in C, \forall y\in \bigcup F, \ x \leq y \Rightarrow x\in \bigcup F$. Let $x\in C$ and $y\in \bigcup F$ and assume $x\leq y$. Then $y\in S$ for some $S\in F$. By definition, $S\sqsubseteq C$, thus $x\in S\subseteq \bigcup F$ as needed.  

??? note "Proof (my version)"

    *Proof.* Let $\mathcal{S}$ be the family of *all* mutual segments of both $C_1$ and $C_2$. By Lemma 2.1, $\bigcup\mathcal{S}\sqsubseteq C_1$ and $\bigcup\mathcal{S}\sqsubseteq C_2$. Thus, $\bigcup\mathcal{S}$ is also a mutual segment, i.e. $\bigcup\mathcal{S}\in \mathcal{S}$, in particular it is the largest mutual segment in the sense that for any mutual segment $S\in \mathcal{S}, \ S\subseteq \bigcup \mathcal{S}$. 

    I claim that either $\bigcup\mathcal{S}$ is either equal to $C_1$ or to $C_2$. Suppose both are not true. Then $\bigcup\mathcal{S} \sqsubset C_1, C_2$ and since both are good chains, $\bigcup\mathcal{S}\sqsubset g(\bigcup\mathcal{S}) \sqsubseteq C_1, C_2$. Thus $g(\bigcup\mathcal{S})$ is a mutual segment, in particular $g(\bigcup\mathcal{S})\subseteq \bigcup\mathcal{S}$, but this contradicts $\bigcup\mathcal{S}\sqsubset g(\bigcup\mathcal{S})$. 

> **Lemma 3.** The union of a family $\mathcal{F}$ of good chains is a good chain.

*Proof.* The union $U := \bigcup \mathcal{F}$ is a chain by comparability. Note that every good chain $D$ such that $D\subseteq U$ is a segment of $U$ : Suppose that $c\in U$ and $c\leq d\in D$. Then $c\in C$ for some good $C\in\mathcal{F}$. If $C$ is a segment of $D$, we have $c\in D$ and are done. Otherwise, the converse relation holds by Comparability and then we also have $c\in D$.

We will see that $U$ is good. Let $S\subset U$ be a proper segment of $U$. Then, there exists $d\in U$ such that $\forall c\in S,\; c<d$. Let $D$ be a good chain such that $d\in D$. Since $D$ is a segment of $U$, all those $c$ belong to $D$. We conclude $S\subseteq D$, and since  $S$ is a segment of $U$, it is a segment of $D$ and it is proper because $d\in D \setminus S$. Then $g(S)$ is segment of $D$, and hence $g(S)$ is a segment of $U$.  

??? note "Prepwork (Lemma 3.1)"

    > *Lemma 3.1.* Let $C$ be a chain and let $S\sqsubset C$ be a proper initial segment, then there exists a $c\in C$ such that $c$ is a strict upper bound of $S$.

    *Proof.* Since $S\subset C$, we can choose a $c$ such that $c\in C$ and $c\notin S$. The claim is that $c$ is a strict upper bound of $S$. Let $s\in S$, then since $s,c\in C$ and $C$ is a chain, either $s\leq c$ or $c\leq s$. If $s\leq c$ then we are done. If $c\leq s$ then $S\sqsubset C$ implies that $c\in S$ which is a contradiction so we are done.

??? note "Prepwork (Lemma 3.2)"

    > *Lemma 3.2.* For any subsets $A, B, C$ of a poset $P$, if $A\sqsubseteq B\sqsubseteq C$ then $A\sqsubseteq C$.

    *Proof.* It is obvious that $A\subseteq C$. Now let $x\in C$ and $y\in A$ such that $x\leq y$. Our goal is to show that $x\in A$. We know that $y\in B$ and so $B\sqsubseteq C$ implies $x\in B$. And finally $A\sqsubseteq B$ implies $x\in A$ as needed.


??? note "Proof (my version)"

    First, we will show that the union $U := \bigcup \mathcal{F}$ is a chain. Let $x,y\in U$, then there are $C_1,C_2$ for which $x\in C_1$ and $y\in C_2$. By comparability and WLOG let $C_1\sqsubseteq C_2$. Then both $x,y\in C_2$ and since $C_2$ is chain, both $x,y$ are comparable, thus $U$ is a chain.

    Next, we will prove an intermediary result : Any good chain $D\subseteq U$ is also an initial segment of $U$.

    Let $c\in U$ and $d\in D$ be such that $c\leq d$. Our goal is to show that $c\in D$. There has to be some good chain $C\in \mathcal{F}$ for which $c\in C$. Now we have two good chains $C,D$ so we can apply comparability. There are two cases :

    - $D\sqsubseteq C$ : If so, then $c\leq d$ implies $c\in D$.
    - $C\sqsubseteq D$ : If so, then $c\in C\subseteq D$.

    In both cases, $c\in D$ so we are done. Now we prove that $U$ is good. Let $S\sqsubset U$ be a proper segment of $U$. By Lemma 3.1 there exists a $d\in U$ such that $d$ is a strict upper bound of $S$. There is a good chain $D\in \mathcal{F}$ such that $d\in D$. We will now prove that $S$ is a proper segment of $D$ :
    
    - By our intermediary result, $D\sqsubseteq U$. Let $c\in S$, then $c<d$ and $D\sqsubseteq U$ implies $c\in D$. Thus $S\subseteq D$.
    - Let $x\in D$ and $y\in S$ such that $x\leq y$, we have to show that $x\in S$. Notice that $x\in U$ and so $S\sqsubset U$ implies that $x\in S$ as needed.
    - Note that $d\in D$ and $d\notin S$ since it is a strict upper bound of $S$. Thus $D\neq S$.

    Since $D$ is a good chain and $S\sqsubset D$, we have $S\sqsubset g(S)\sqsubseteq D$. We combine this with the fact that $D\sqsubseteq U$ and Lemma 3.2 to get $S\sqsubset g(S)\sqsubseteq U$ as required. Thus $U$ is good.


By considering the union of *all* good chains, we readily obtain :

> **Theorem 4.** (Greatest Good Chain). Let $P$ be a poset and $g: \mathcal{P}(P) \to \mathcal{P}(P)$. The family of all good
  chains has a maximum under inclusion.

??? note "Proof (my version)"

    More explicitly : Let $\mathcal{G}$ be the family of all good chains for a given poset $P$ and function $g$. We need to prove that there exists a chain $M\in \mathcal{G}$ such that for any other good chain $C\in \mathcal{G}, C\subseteq M$.

    I claim that $M = \bigcup \mathcal{G}$ works. By Lemma 3, $M$ is a good chain. Furthermore, for any $C\in \mathcal{G}$, by definition $C\subseteq \bigcup \mathcal{G} = M$. Thus $M$ is the "maximum" element we are looking for. 

## Chain Bounding and Applications

The following lemma is the key to all of what follows. In some sense, it might be regarded as a non-$AC$ version of Zorn's lemma.

> **Lemma 5.** (Chain Bounding). Let $P$ be a poset. There is no assignment of a strict upper bound to each chain in $P$.

*Proof.* Assume, by way of contradiction, that $f(C)$ is a strict upper bound of $C$ for each chain $C\subseteq P$. Hence $C$ is a proper segment of $g(C) := C\cup \{f(C)\}$; extend this $g$ arbitrarily to the rest of the subsets of $P$. By Theorem 4, there exists a greatest good chain $U$ for $g$. But this is a contradiction, since $g(U)$ is easily seen to be a good chain, but $g(U)\not\subseteq U$.

??? note "Proof (my version)"

    We prove this by contradiction. Suppose each chain $C$ in $P$ is associated with a strict upper bound which we denote $f(C)$. We define a function $g:\mathcal{P}(P)\to \mathcal{P}(P)$ where

    $$ g(C) := \begin{cases}
        C\cup \{f(C)\} &, \text{ if } C \text{ is a chain} \\
        \varnothing &, \text{ otherwise}
    \end{cases} $$

    By Theorem 4 there exists a greatest good chain $U$ for $g$. We will now prove that $g(U)$ is a good chain. That $g(U)$ is a chain is easy to show and I will leave you to figure out the details for yourself.

    > **Lemma 5.1.** We will show that every chain $C$ is a proper segment of $g(C)$. 
    >
    > - *Proof.* Obviously $C\subset g(C)$. Now let $x\in g(C)$ and $y\in C$ be such that $x\leq y$. Our goal is to show that $x\in C$. Suppose $x\notin C$ then $x=f(C)$, but this contradicts $x\leq y$, thus we must have $x\in C$ as required.
    >
    > **Lemma 5.2.** Let $S$ be a proper segment of $g(U)$, we will show that $S\sqsubseteq U$. 
    >
    > - *Proof.* Recall that $g(U) = U\cup \{f(U)\}$ by definition. We start by showing that $f(U)\not\in S$. If it is, then $S\sqsubset g(U)$ and the fact that $u\leq f(U)$ for all $u\in g(U)$ would imply that $u\in S$ for all $u\in g(U)$. Thus $S=g(U)$ but this contradicts $S$ being a proper segment. Thus, $S\subseteq U$. Now let $x\in U$ and $y\in S$ such that $x\leq y$. Notice that $x\in g(U)$ and $S\sqsubset g(U)$, thus $x\in S$ and hence $S\sqsubseteq U$ as required.

    We now show that $g(U)$ is good. Let $S$ be a proper segment of $g(U)$, then by Lemma 5.2, $S\sqsubseteq U$. By definition, either $S=U$ or $S\sqsubset U$. 

    - Case 1 ($S=U$) : By Lemma 5.1, $U\sqsubset g(U)$ and obviously $g(U)\sqsubseteq g(U)$, thus $g(U)$ is good.

    - Case 2 ($S\sqsubset U$) : Since $U$ is good, $S \sqsubset g(S)\sqsubseteq U$. Furthermore, we have $U\sqsubset g(U)$ from Lemma 5.1. Applying Lemma 3.2 gives $S \sqsubset g(S)\sqsubseteq g(U)$, thus $g(U)$ is good.
    
    Since we have shown that $g(U)$ is a good chain, we must have $g(U)\subseteq U$ by maximality of $U$, but $g(U)$ has to be strictly larger than $U$ by definition of $g$, and thus we have our contradiction.
 
The wording of the Chain Bounding Lemma is a bit awkward, since it is actually a negation. However, if we now invoke $AC$, we get the following more natural statement.

> **Lemma 6.** (Unbounded Chain). Assume $AC$. For every poset $P$ there exists a chain $C\subseteq P$ with no strict upper bound.

*Proof.* By way of contradiction, assume that for every chain $C\subseteq P$ there exists a strict upper bound. Using $AC$, let $f$ assign to each $C$ such a bound. But this contradicts Chain Bounding.

> **Corollary 7.** (Zorn). If a poset $P$ contains an upper bound for each chain, it has a maximal element.

*Proof.* By the Unbounded Chain lemma, take $C\subseteq P$ without strict upper bounds. Then any upper bound of $C$ must be maximal in $P$.

??? note "Proof (my version)"

    I will just be clarifying some points. By "maximal in $P$" we mean a point $x\in P$ for which there cannot exist a $y\in P$ for which $x<y$. $C$ has an upper bound by assumption, call it $u$. Now suppose there is a $y\in P$ for which $u<y$. Since $u$ is an upper bound of $C$, $y$ has to be strict upper bound of $C$, but $C$ has no strict upper bounds by assumption. Thus $u$ is maximal in $P$. 

---

**Corollary 10.** (Bourbaki-Witt). Let $P$ be a nonempty poset such that every chain $C\subseteq P$ has a least upper bound. If $h:P\to P$ satisfies $x\leq h(x)$ for all $x\in P$, then $h$ has a fixed point, i.e., there is some $x\in P$ such that $x=H(x)$.

*Proof.* Assume by way of contradiction that $x<h(x)$ for all $x\in P$. But then $f(C):=h(\sup C)$ immediately contradicts Chain Bounding.

??? note 

    The proof here is easy to follow, but there are some subtleties I'd like to comment on. Bourbaki-Witt doesn't require AoC, only Lemma 6 (which is used to prove Zorn's Lemma) requires assuming AoC. To understand this bit of detail more, let us analyze the requirement that every chain $C$ has a least upper bound. If we relax this to "has an upper bound", then we will get stuck when defining $f$ because we would have to *choose* an upper bound of $C$ to feed into $h$; of course we can make this choice, but only if we assume AoC. Since the least upper bound is unique, there is no choice involved so we can avoid assuming AoC. 

