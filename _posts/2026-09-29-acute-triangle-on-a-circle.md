---
layout: post
title: An Acute Triangle on a Circle
date: 2026-09-29 12:03:00+0800
description: Interesting Problem in Quant Interview
tags: probability geometry
categories: quant
---

# Problem.

Three points are chosen independently and uniformly on the circumference of a circle. What is the probability that they form an acute triangle?

# Solution.

### 1. Translate the angle condition into a semicircle condition

Let $G_1,G_2,G_3$ be the angular lengths of the arcs between successive sampled points, so $G_1+G_2+G_3=2\pi$. By the inscribed-angle theorem, the triangle's angles are $G_1/2,G_2/2,G_3/2$, in the corresponding opposite order. Hence

$$
\text{the triangle is acute}
\quad\Longleftrightarrow\quad
\max\{G_1,G_2,G_3\}<\pi.
$$

A gap greater than $\pi$ leaves all three points on a complementary arc shorter than $\pi$, and conversely. Thus the triangle is obtuse exactly when its vertices lie in some open semicircle.

Coincident points and antipodal pairs have probability zero. Right triangles therefore have probability zero, and the acute-triangle probability is the complement of the semicircle probability.

### 2. Anchor the semicircle at a sampled point

Label the original sampled points $P_1,P_2,P_3$. For each $i$, let $A_i$ be the event that both other points lie in the clockwise open semicircle beginning at $P_i$. Conditional on $P_i$, each of the two other points independently falls in that semicircle with probability $1/2$. Hence

$$
\mathbb P(A_i)=\left(\frac12\right)^2=\frac14.
$$

If the points fit in an open semicircle, its first sampled point in clockwise order is an anchor for which $A_i$ holds. Conversely, each $A_i$ puts all three points in some open semicircle. Thus the semicircle event is $A_1\cup A_2\cup A_3$.

The events $A_i$ are pairwise disjoint. If both $A_i$ and $A_j$ held, the clockwise angular distance from $P_i$ to $P_j$ and the clockwise distance back from $P_j$ to $P_i$ would both be less than $\pi$. This is impossible because they sum to $2\pi$.

Consequently, the semicircle event has probability $\sum_{i=1}^3\mathbb P(A_i)=3/4$, and

$$
\boxed{\mathbb P(\text{acute})=1-\frac34=\frac14.}
$$

**Related post.** [All Points in a Semicircle](https://myzhong-cuhk.github.io/blog/2026/semicircle/) gives the general probability $N/2^{N-1}$ for $N$ independent uniform points. This problem uses its $N=3$ case and takes the complement.
