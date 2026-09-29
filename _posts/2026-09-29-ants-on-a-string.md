---
layout: post
title: Ants on a String
date: 2026-09-29 12:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

500 ants are randomly put on a 1-foot string (independent uniform distribution for each ant between 0 and 1). Each ant randomly moves toward one end of the string (equal probability to the left or right) at constant speed of 1 foot/minute until it falls off at one end of the string. Also assume that the size of the ant is infinitely small. When two ants collide head-on, they both immediately change directions and keep on moving at 1 foot/min. What is the expected time for all ants to fall off the string?

# Solution.

The key observation is that **a collision is equivalent to exchanging labels**. If we swap the two ants' labels whenever they collide and reverse direction, each label continues moving in its original direction. The occupied positions and all departure times are unchanged. Thus, we may calculate the time until the string is empty by letting the ants pass straight through one another.

In this equivalent model, let $X_i\sim\operatorname{Unif}[0,1]$ be the initial position of ant $i$. Its departure time, measured in minutes, is

$$
T_i=
\begin{cases}
X_i,&\text{if it initially moves left},\\
1-X_i,&\text{if it initially moves right}.
\end{cases}
$$

For $0\leq t\leq1$,

$$
\mathbb P(T_i\leq t)
=\frac12\mathbb P(X_i\leq t)
+\frac12\mathbb P(X_i\geq1-t)
=\frac12t+\frac12t=t.
$$

Therefore $T_i\sim\operatorname{Unif}[0,1]$. The initial positions and direction choices are independent across ants, so the departure times in this equivalent model are also independent.

All ants have fallen off when the last one leaves. Hence

$$
T=\max_{1\leq i\leq500}T_i,
\qquad
\mathbb P(T\leq t)
=\prod_{i=1}^{500}\mathbb P(T_i\leq t)
=t^{500},
\quad 0\leq t\leq1.
$$

Using the tail-integral formula for a nonnegative random variable,

$$
\boxed{
\mathbb E[T]
=\int_0^1\mathbb P(T>t)\,dt
=\int_0^1(1-t^{500})\,dt
=\frac{500}{501}\text{ minutes}.
}
$$
