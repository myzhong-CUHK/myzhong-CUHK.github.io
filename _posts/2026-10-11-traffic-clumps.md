---
layout: post
title: Traffic Clumps and Record Minima
date: 2026-10-11 00:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

You have N cars that are all traveling in the same direction on an infinitely long one-lane highway. Unfortunately, they are all going at different speeds and cannot pass each other. Eventually, the cars will clump up in one or more traffic jams. In terms of N, what is the expected number of clumps of cars?

# Solution.

### 1. Clumps correspond to record minima

Index the cars **from front to back**, with distinct desired speeds $v_1,\ldots,v_N$. Assume finite initial gaps and a uniformly random ordering of the speeds; i.i.d. continuous speeds also satisfy the ordering assumption. Each car keeps its desired speed until it catches a slower clump, whose speed it then adopts.

Let $C_N$ be the eventual number of clumps, and define

$$
m_0=+\infty,
\qquad
m_i=\min_{1\leq j\leq i}v_j.
$$

Inductively, the rearmost clump among the first $i-1$ cars eventually travels at speed $m_{i-1}$. If $v_i<m_{i-1}$, car $i$ cannot catch any clump ahead and starts a new clump. If $v_i>m_{i-1}$, its positive relative speed and the finite gap ensure that it eventually joins the rearmost clump ahead. Hence the clump leaders are exactly the **record minima**:

$$
I_i:=\mathbf1_{\{v_i<m_{i-1}\}},
\qquad I_1=1,
\qquad
C_N=\sum_{i=1}^N I_i.
$$

For the example, read $3,1,4,6,8,2,7,9,5$ from front to back. Its record minima are $3$ and $1$, so there are two clumps: the first car, and a clump led by the car of speed $1$ containing every remaining car.

### 2. Take expectations

Under a uniformly random ordering, each of the first $i$ positions is equally likely to contain their minimum. Therefore

$$
\mathbb P(I_i=1)
=\mathbb P\!\left(v_i=\min_{1\leq j\leq i}v_j\right)
=\frac1i.
$$

Linearity of expectation gives

$$
\boxed{
\mathbb E[C_N]
=\sum_{i=1}^N\mathbb E[I_i]
=\sum_{i=1}^N\frac1i
=H_N.
}
$$

No independence assumption between the indicators is needed for this step.
