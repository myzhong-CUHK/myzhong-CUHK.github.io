---
layout: post
title: Three Bags of Coins
date: 2026-09-13 22:00:00+0800
description: Interesting Problem in Quant Interview
tags: brainteaser
categories: quant
---

# Problem.

There are three bags, each holding plenty of gold coins. Within a bag all coins weigh the same, and every weight is a positive integer number of grams. You have an exact electronic scale with unlimited range. In each weighing you may take any finite number of coins (possibly zero) from each bag, read the total weight, and use the result to decide the next weighing.

The following questions are independent. In each one, find the minimum number of weighings, and explain the method and the reason.

1. One bag's coins weigh $9$ or $11$ grams; the other two bags' coins weigh $10$ grams. Find the abnormal bag and whether its coins are light or heavy.
2. One bag's coins differ from the other two by $1$ gram; the normal weight is unknown. Find the abnormal bag and whether its coins are light or heavy.
3. Determine the per-coin weight of each of the three bags.

# Solution.

Call the bags $A$, $B$, $C$ and write $w_A, w_B, w_C$ for the per-coin weights, all positive integers. A weighing with $a$ coins from $A$, $b$ from $B$ and $c$ from $C$ returns

$$
S = a\,w_A + b\,w_B + c\,w_C .
$$

The whole game is choosing $(a, b, c)$ so that $S$ decodes the unknowns. One lower bound is used throughout: zero weighings give no information, so whenever at least two states are possible, at least one weighing is needed.

### Part 1: Take one, two and three coins

There are $3 \times 2 = 6$ states: which bag is abnormal, and whether it is light or heavy. Write $\delta \in \{-1, +1\}$ for the deviation and $x$ for the number of coins taken from the abnormal bag, so $x \in \{a, b, c\}$. Then

$$
S = 10\,(a + b + c) + \delta x .
$$

Take $(a, b, c) = (1, 2, 3)$: one coin from $A$, two from $B$, three from $C$. Then

$$
S - 60 = \delta x \in \{-3, -2, -1, 1, 2, 3\},
$$

and the six states give six different readings.

- $S = 59, 58, 57$ means $A$, $B$, $C$ is **light**.
- $S = 61, 62, 63$ means $A$, $B$, $C$ is **heavy**.

The sign of $S - 60$ says light or heavy, and its size says which bag. Any three **distinct positive** counts would work; $(0, 1, 2)$ would not, because $x = 0$ hides the deviation completely.

Since zero weighings cannot separate six states, the minimum is $1$ weighing.

### Part 2: Make the unknown weight disappear modulo 7

Now the normal weight $w$ is an unknown positive integer, the abnormal bag weighs $w + \delta$ with $\delta \in \{-1, +1\}$, and a weighing gives

$$
S = w\,(a + b + c) + \delta x, \qquad x \in \{a, b, c\} .
$$

Look at the nuisance term. It is an unknown multiple of $N := a + b + c$, so it vanishes **modulo** $N$:

$$
S \equiv \delta x \pmod N .
$$

We therefore need the six residues $\pm a, \pm b, \pm c$ to be pairwise distinct modulo $N$. Conversely, if two different states have the same residue, write $\delta_1 x_1 - \delta_2 x_2 = kN$; then normal weights $w$ and $w + k$ (with $w$ large enough that both are at least $2$) give the same $S$, so distinctness is also necessary. The choice $(1, 2, 3)$ from Part 1 fails: $N = 6$ and $+3 \equiv -3 \pmod 6$, so "$C$ heavy with normal weight $w$" and "$C$ light with normal weight $w + 1$" both give $S = 6w + 3$ and cannot be told apart.

Take instead $(a, b, c) = (1, 2, 4)$, so $N = 7$.

- $S \bmod 7 = 1, 2, 4$ means $A$, $B$, $C$ is **heavy**.
- $S \bmod 7 = 6, 5, 3$ means $A$, $B$, $C$ is **light**.

All six residues are distinct, so one weighing decides both the bag and the direction. As a bonus, $w = (S - \delta x)/7$.

For example, if $w = 10$ and $C$ is light, then $S = 70 - 4 = 66 \equiv 3 \pmod 7$, which decodes correctly to "$C$, light". Zero weighings is again impossible, so the minimum is $1$ weighing.

Six distinct classes $\pm a, \pm b, \pm c$ cannot fit in $\mathbb{Z}/N\mathbb{Z}$ for $N \leq 6$ when $a + b + c = N$, so $N \geq 7$ and $(1, 2, 4)$ even uses the fewest coins possible.

### Part 3: One weighing is never enough

A single weighing with any $(a, b, c)$ shows one integer $S = a\,w_A + b\,w_B + c\,w_C$. Split on how many coefficients are positive.

- If **at least two** coefficients are positive, say $a, b > 0$, then the distinct triples $(w_A + b, \; w_B, \; w_C)$ and $(w_A, \; w_B + a, \; w_C)$ give the same $S$.
- If **at most one** coefficient is positive, two of the weights are never seen at all.

Either way $S$ cannot determine the triple $(w_A, w_B, w_C)$.

The obstruction is that the weights are **unbounded**: a fixed base like $(1, 10^3, 10^6)$ works only if $w_A$ and $w_B$ are known in advance to be below $10^3$. The way out is to let the first weighing produce a bound, and the second one exploit it.

### Part 3: Two weighings, the first one picks the base

For the first weighing, take one coin from each bag:

$$
S_1 = w_A + w_B + w_C .
$$

Since all weights are positive integers, $1 \leq w_B, w_C \leq S_1 - 2 < S_1$.

For the second weighing, take one coin from $B$ and $S_1$ coins from $C$:

$$
S_2 = w_B + S_1\,w_C .
$$

Because $1 \leq w_B < S_1$, the pair $(w_B, w_C)$ is exactly the **base**-$S_1$ representation of $S_2$:

$$
w_C = \left\lfloor \frac{S_2}{S_1} \right\rfloor,
\qquad
w_B = S_2 - S_1\,w_C,
\qquad
w_A = S_1 - w_B - w_C .
$$

For example, if $(w_A, w_B, w_C) = (7, 12, 5)$, then $S_1 = 24$ and $S_2 = 12 + 24 \cdot 5 = 132$. Indeed $132 = 5 \cdot 24 + 12$, so $w_C = 5$, $w_B = 12$ and $w_A = 24 - 12 - 5 = 7$.

Two weighings suffice and one does not, so the minimum is $2$ weighings.
