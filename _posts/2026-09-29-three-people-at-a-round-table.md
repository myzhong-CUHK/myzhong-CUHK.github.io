---
layout: post
title: Three People at a Round Table
date: 2026-09-29 12:02:00+0800
description: Interesting Problem in Quant Interview
tags: probability combinatorics
categories: quant
---

# Problem.

Three people choose three distinct seats uniformly at random around a circular table with eight seats. What is the probability that at least two of them sit next to each other?

# Solution.

Number the seats $1,\ldots,8$ clockwise, with seats $8$ and $1$ adjacent. There are $\binom83=56$ equally likely sets of three occupied seats, since each set allows the same $3!$ assignments of people. Let $N$ be the number of these sets with **no adjacent occupied seats**. The required probability is $1-N/56$.

To count $N$, temporarily mark one occupied seat as the starting point. Reading clockwise from it, let $g_1,g_2,g_3$ be the numbers of empty seats between successive occupied seats, including the gap back to the start. The five empty seats must form three nonempty gaps:

$$
g_1+g_2+g_3=5,
\qquad g_i\geq1.
$$

Stars and bars gives $\binom{5-1}{3-1}=\binom42=6$ ordered gap triples. There are $8$ choices for the starting seat, and each starting seat and gap triple determines a configuration. This gives $8\binom42$ configurations with a marked starting seat.

Each occupied-seat set is counted exactly $3$ times, because any of its three occupied seats can be marked as the start. For example, the set $\{1,3,5\}$ is counted once starting at $1$, once at $3$, and once at $5$. Therefore,

$$
N=\frac{8\binom42}{3}=16.
$$

Taking the complement,

$$
\boxed{
\mathbb P(\text{at least one adjacent pair})
=1-\frac{16}{56}
=\frac57.
}
$$

**Related post.** The positive-gap count is an application of [Stars and Bars -- Empty and Nonempty Groups](https://myzhong-cuhk.github.io/blog/2026/stars-and-bars/).
