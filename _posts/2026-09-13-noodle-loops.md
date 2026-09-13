---
layout: post
title: Noodle Loops
date: 2026-09-13 23:30:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

You have $100$ noodles in your soup bowl. Being blindfolded, you are told to take two ends of some noodles (each end on any noodle has the same probability of being chosen) in your bowl and connect them. You continue until there are no free ends. The number of loops formed by the noodles this way is stochastic. Calculate the expected number of circles.

# Solution.

Let $n$ be the number of noodles ($n = 100$), so there are $2n$ free ends at the start. Every tie uses up two free ends, so after exactly $n$ ties nothing is left: the process always has $n$ steps.

Call a **strand** any chain of noodles that have been tied end to end but is not yet closed. A strand has exactly two free ends, just like a single noodle. At the start there are $n$ strands. When we tie two free ends, one of two things happens.

- The two ends belong to the **same** strand. The strand closes into a loop and drops out of the game.
- The two ends belong to **different** strands. The two strands merge into one longer strand.

Either way the number of strands goes down by exactly one. So **just before** the $j$-th tie is made there are $i = n - (j - 1)$ strands in the bowl and $2i$ free ends, and just after it there are $i - 1$. Counted this way, the $n$ ties are made with $n, n - 1, \dots, 2, 1$ strands present; the last tie is made with a single strand, and closes it.

### Method 1: One indicator per tie

Look at the tie made when $i$ strands and $2i$ free ends are present (that is, just before this tie). Pick the first end; whichever it is, the second end is uniform over the other $2i - 1$ free ends, and exactly **one** of them is the other end of the same strand. So

$$
\mathbb{P}(\text{this tie closes a loop}) = \frac{1}{2i - 1},
$$

whatever happened before. Let $I_i$ be the indicator that the tie made with $i$ strands present closes a loop. The number of loops is $L = I_n + I_{n-1} + \cdots + I_1$, and by linearity of expectation

$$
\mathbb{E}[L] = \sum_{i = 1}^{n} \frac{1}{2i - 1} = 1 + \frac{1}{3} + \frac{1}{5} + \cdots + \frac{1}{2n - 1} .
$$

For $n = 100$,

$$
\mathbb{E}[L] = 1 + \frac{1}{3} + \frac{1}{5} + \cdots + \frac{1}{199} .
$$

The last term is $I_1 = 1$: when a single strand is left, its two ends must be tied to each other.

### Method 2: Condition on the first tie

Write $E_n$ for the expected number of loops with $n$ noodles. The first tie joins a uniformly chosen pair among $2n$ ends.

- With probability $\tfrac{1}{2n - 1}$ the two ends belong to the same noodle. One loop is done, and $n - 1$ untouched noodles remain.
- Otherwise two different noodles are joined into one long strand. Now there are $n - 1$ strands, each with two free ends, and the blindfolded process does not care whether a strand is one noodle or two: from here on it is exactly the game with $n - 1$ noodles.

Hence

$$
E_n = \frac{1}{2n - 1} + E_{n - 1}, \qquad E_1 = 1 ,
$$

and unrolling the recursion gives the same sum $E_n = \sum_{i=1}^{n} \tfrac{1}{2i - 1}$.
