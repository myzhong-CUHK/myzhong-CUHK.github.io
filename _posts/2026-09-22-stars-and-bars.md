---
layout: post
title: Stars and Bars -- Empty and Nonempty Groups
date: 2026-09-22 01:53:47+0800
description: Interesting Problem in Quant Interview
tags: combinatorics
categories: quant
---

Suppose we distribute $n$ **identical objects** among $m$ **distinct groups**, where $n\geq 0$ and $m\geq 1$ are integers.

If $x_i$ is the number of objects in group $i$, then

$$
x_1+x_2+\cdots+x_m=n.
$$

The groups are distinguished by their positions: for example, $(1,1,3)$ and $(3,1,1)$ are different allocations. The objects themselves are not labeled, so exchanging two objects within an allocation does not create a new one.

The **stars and bars** method represents the objects by stars and separates consecutive groups with bars. There are $n$ stars and $m-1$ bars.

### 1. Empty groups are allowed

We first count the nonnegative integer solutions of

$$
x_1+x_2+\cdots+x_m=n,
\qquad x_i\geq 0.
$$

For example, when $n=5$ and $m=3$, the following arrangements represent different allocations:

```text
||*****   <-> (0, 0, 5)
**||***   <-> (2, 0, 3)
*|*|***   <-> (1, 1, 3)
*****||   <-> (5, 0, 0)
```

A bar at the beginning or end creates an empty group. Two adjacent bars create an empty group between them. All these arrangements are allowed.

Every allocation corresponds to exactly one arrangement of stars and bars, and every such arrangement determines exactly one allocation. Thus, it suffices to count the arrangements.

There are $n+m-1$ positions in total. Choose $m-1$ of them for the bars; the remaining positions contain stars. Therefore,

$$
\boxed{
\#\{(x_1,\ldots,x_m):x_1+\cdots+x_m=n,\ x_i\geq 0\}
=\binom{n+m-1}{m-1}.
}
$$

We do not multiply by $(m-1)!$: the bars have no individual labels. Only their positions matter.

For $n=5$ and $m=3$, the count is

$$
\boxed{
\binom{5+3-1}{3-1}
=\binom{7}{2}
=21.
}
$$

### 2. Every group must be nonempty

Now consider the positive integer solutions of

$$
x_1+x_2+\cdots+x_m=n,
\qquad x_i\geq 1.
$$

If $n<m$, there are too few objects to give one to every group, so the count is zero. Suppose henceforth that $n\geq m$.

Place the $n$ stars in a row. There are exactly $n-1$ internal gaps between consecutive stars. To form $m$ nonempty groups, choose $m-1$ distinct internal gaps and put one bar in each.

For five stars, the four available gaps are

```text
* _ * _ * _ * _ *
```

Bars cannot be placed at either end, and two bars cannot occupy the same gap: either choice would create an empty group. Consequently,

$$
\boxed{
\#\{(x_1,\ldots,x_m):x_1+\cdots+x_m=n,\ x_i\geq 1\}
=
\begin{cases}
\displaystyle\binom{n-1}{m-1}, & n\geq m,\\[6pt]
0, & n<m.
\end{cases}
}
$$

For $n=5$ and $m=3$, this gives

$$
\boxed{
\binom{5-1}{3-1}
=\binom{4}{2}
=6.
}
$$

The six allocations are

$$
(1,1,3),\quad (1,2,2),\quad (1,3,1),\quad
(2,1,2),\quad (2,2,1),\quad (3,1,1).
$$
