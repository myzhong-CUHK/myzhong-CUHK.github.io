---
layout: post
title: Meeting in the Final
date: 2026-09-03 01:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

A knockout tournament has $2^n$ players with skills $1 > 2 > \dots > 2^n$, the stronger player always winning. Except for the final, the opponents in each round are drawn at random among the survivors. What is the probability that players $1$ and $2$ meet in the final?

# Solution.

Two remarks fix the shape of the problem. Player $1$ beats everybody, so player $1$ reaches the final no matter what the draw does. Player $2$ beats everybody except player $1$, so player $2$ survives every round until the round in which the two are drawn against each other.

So the two of them meet exactly once, in some round $k \in \{1, \dots, n\}$, and the question asks for the probability that $k = n$.

### Method 1: Round by round

A round that starts with $m$ survivors pairs them into a uniformly random perfect matching, so the opponent of player $1$ is uniform among the other $m-1$ players and

$$
\mathbb{P}(\text{the two are drawn together}) = \frac{1}{m-1}.
$$

If they are not drawn together both of them win and both survive, so the rounds simply multiply. Round $j$ counted from the end has $2^{j}$ players, and avoiding each other in all rounds but the final means avoiding each other for $j = n, n-1, \dots, 2$:

$$
p_n
= \prod_{j=2}^{n}\frac{2^{j}-2}{2^{j}-1}
= \frac{2^{\,n-1}}{2^{n}-1} .
$$

### Method 2: The two halves

A finished tournament always falls into two halves of $2^{\,n-1}$ players. Players $1$ and $2$ reach the final together exactly when they lie in **different halves**, and player $2$ is equally likely to sit in any of the $2^{n}-1$ places other than player $1$'s, and $2^{\,n-1}$ of those lie in the opposite half. Hence

$$
p_n = \frac{2^{\,n-1}}{2^{n}-1} .
$$

