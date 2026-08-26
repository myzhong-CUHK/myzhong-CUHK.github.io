---
layout: post
title: Uniform Sum
date: 2026-08-24 10:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

**Problem.** Numbers are drawn uniformly at random from $[0, 1]$ until their sum
exceeds $1$. Find the expected value of the last number drawn.

**Solution.** Let $X_1, X_2, \dots \sim \mathcal{U}(0, 1)$ be i.i.d., and for
$a \in [0, 1]$, let $T(a) = \inf\\{m : \sum_{i=1}^m X_i \geq a\\}$. Denote
$f(a) = \mathbb{E}[X_{T(a)}]$.

Conditioning on the first draw, $\mathbb{E}[X_{T(a)}] = \mathbb{E}\left[\mathbb{E}[X_{T(a)} \mid X_1]\right]$, where

$$
\mathbb{E}[X_{T(a)} \mid X_1]
=
\begin{cases}
X_1 & \text{if } X_1 \geq a, \\
X_{T(a - X_1)} & \text{otherwise.}
\end{cases}
$$

Taking expectations gives

$$
f(a) = \int_a^1 x \, dx + \int_0^a f(a - x)  dx,
$$

with $f(0) = \frac{1}{2}$. Differentiating turns it into an ODE,

$$
f'(a) = f(a) - a , \qquad f(0) = \frac{1}{2} ,
$$

whose solution is

$$
f(a) = a + 1 - \frac{1}{2} e^{a} .
$$

Therefore

$$
\mathbb{E}[X_{T(1)}] = f(1) = 2 - \frac{e}{2} .
$$
