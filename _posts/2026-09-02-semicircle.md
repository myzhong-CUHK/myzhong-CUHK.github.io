---
layout: post
title: All Points in a Semicircle
date: 2026-09-01 10:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

Given $N$ points drawn independently and uniformly on the circumference of a circle, what is the probability that all of them lie within some semicircle?

# Solution.

Normalise the circumference to $1$, so a semicircle is an arc of length $\tfrac12$ and the points are i.i.d. uniform on $[0,1)$. With probability one no two points coincide and no two are
antipodal, so the degenerate cases can be ignored throughout.

### Method 1: Anchor at each point

For each $i$, let $A_i$ be the event that all the other $N-1$ points lie in the half-circle running
clockwise from point $i$. In words, point $i$ is the "first" point of the cluster.

**Each $A_i$ has probability $2^{-(N-1)}$.** Condition on where point $i$ landed. The remaining $N-1$ points are independent and uniform, and each falls in the specified half-circle with probability $\tfrac12$. 

**The events are mutually exclusive.** Suppose $A_i$ and $A_j$ both held for $i \neq j$. Write $\theta$ for the clockwise distance from $i$ to $j$. Since $A_i$ holds, $\theta < \tfrac12$. But then the clockwise distance from $j$ back to $i$ is $1 - \theta > \tfrac12$, so point $i$ is outside the half-circle clockwise from $j$, contradicting $A_j$.

Therefore,

$$
p_N = \sum_{i=1}^{N} \mathbb{P}(A_i) = \frac{N}{2^{N-1}} .
$$


### Method 2: The largest gap

The $N$ points cut the circle into $N$ arcs. Call their lengths $G_1, \dots, G_N$, with $G_1 + \cdots + G_N = 1$.

All the points lie in a semicircle exactly when some gap has length at least $\frac12$. Two gaps cannot both reach $\tfrac12$ without exhausting the whole circle, so again the events are disjoint and

$$
p_N = \mathbb P \left( \bigcup_{i=1}^N \left\{G_i \geq \frac12\right\}\right) = \sum_{i=1}^{N} \mathbb{P}\left(G_i \geq \frac12\right) = \frac{N}{2^{N-1}},
$$

using $\mathbb{P}(G_i \geq x) = (1-x)^{N-1}$.
