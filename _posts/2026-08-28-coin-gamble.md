---
layout: post
title: One More Coin
date: 2026-08-28 10:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem. 

Gambler $A$ has $N+1$ fair coins and gambler $B$ has $N$. Both toss all of their coins. What is the probability that $A$ gets strictly more heads than $B$?

# Solution.

Write $A$ and $B$ for the two head counts, so $A \sim \mathrm{Bin}(N+1, \tfrac12)$ and $B \sim \mathrm{Bin}(N, \tfrac12)$ are independent. The event of interest is $\{A > B\}$.

### Method 1: Pool all the coins

Since the counts are integers, $A > B$ is the same as $A - B \geq 1$, which after adding $N$ to both sides reads

$$
A + (N - B) \geq N + 1 .
$$

Look at what the left side counts. The term $A$ is the number of **heads** among $A$'s $N+1$ coins, and $N - B$ is the number of **tails** among $B$'s $N$ coins. Every one of the $2N+1$ coins on the table contributes independently, and each contributes with probability $\tfrac12$. So

$$
W := A + (N - B) \sim \mathrm{Bin}\left(2N+1, \tfrac12\right),
$$

and the question becomes whether $W$ exceeds half of $2N+1$.

Now $2N+1$ is **odd**, so $W \geq N+1$ and $W \leq N$ are complementary and have the same probability.

$$
\mathbb{P}(A > B) = \mathbb{P}(W \geq N+1) = \frac{1}{2}.
$$

### Method 2: Exchange heads and tails

Let $A' = (N+1) - A$ and $B' = N - B$ be the two tail counts. Then

$$
A' > B'
\iff (N+1) - A > N - B
\iff B + 1 > A
\iff A \leq B .
$$

So $\{A > B\}$ and $\{A' > B'\}$ are complementary: exactly one of them happens, always.

Because the coins are fair, $\mathbb{P}(A' > B') = \mathbb{P}(A > B)$. Two events that are complementary and equally likely, so each have probability $\tfrac12$.

### Method 3: Condition on the extra coin

Let $A$ toss $N$ coins first, giving $A_N$, and call the last coin $\varepsilon \in \{0,1\}$, so that $A = A_N + \varepsilon$. Now we have

$$
p := \mathbb{P}(A_N > B) = \mathbb{P}(A_N < B), \qquad q := \mathbb{P}(A_N = B), \qquad 2p + q = 1 .
$$

Split on the first $N$ tosses.

- If $A_N > B$, then $A \geq A_N > B$ whatever the last coin does. $A$ wins.
- If $A_N = B$, then $A$ wins exactly when $\varepsilon = 1$, which has probability $\tfrac12$.
- If $A_N < B$, then $A_N \leq B - 1$, so even $A_N + 1 \leq B$. $A$ cannot win.

Hence

$$
\mathbb{P}(A > B) = p + \frac{q}{2} = \frac{1}{2}.
$$
