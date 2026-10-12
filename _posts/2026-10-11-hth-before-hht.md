---
layout: post
title: HTH Before HHT -- A Pattern Race
date: 2026-10-11 12:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

A fair coin is tossed independently. What is the probability that $HTH$ appears as three consecutive outcomes before $HHT$ does?

# Solution.

Let $\tau_{HTH}$ and $\tau_{HHT}$ be the numbers of tosses needed for the first complete occurrences of the respective patterns. Define

$$
W:=\{\tau_{HTH}<\tau_{HHT}\},
\qquad
p:=\mathbb P(W).
$$

### Method 1. Restart after an unsuccessful attempt

Ignore any initial tails and wait for the first head. Neither pattern can appear before this head, so the probability of eventually winning from this point is still $p$.

Starting from this first $H$, there are three possibilities:

- The next toss is $H$, with probability $1/2$. Once the sequence ends in $HH$, every additional head preserves that suffix, and the first subsequent tail completes $HHT$. Thus $HTH$ cannot win along this branch.
- The next two tosses are $TH$, with probability $1/4$. They complete $HTH$, so we win immediately.
- The next two tosses are $TT$, with probability $1/4$. The sequence ends in $HTT$, neither target has appeared, and no nonempty suffix is a beginning of either target. We therefore start afresh, with winning probability $p$.

By conditioning on these three possibilities,

$$
p=\frac12\cdot0+\frac14\cdot1+\frac14p.
$$

Consequently,

$$
\boxed{\mathbb P(\tau_{HTH}<\tau_{HHT})=p=\frac13.}
$$

### Method 2. Conditional probabilities given initial tosses

Use $\mathbb P(W\mid H)$ to mean the probability of $W$ conditional on the first toss being $H$; similarly, $\mathbb P(W\mid HT)$ conditions on the first two tosses being $HT$. These conditions specify the initial prefix of the sequence.

Conditioning on the first toss gives

$$
p=\frac12\mathbb P(W\mid H)+\frac12\mathbb P(W\mid T).
$$

An initial tail contributes no progress toward either pattern, and subsequent tosses are independent of it. Hence

$$
\mathbb P(W\mid T)=p,
\qquad
\mathbb P(W\mid H)=p.
$$

Next, condition on the second toss:

$$
\mathbb P(W\mid H)
=\frac12\mathbb P(W\mid HH)
+\frac12\mathbb P(W\mid HT).
$$

As in Method 1, an initial $HH$ guarantees that $HHT$ wins when the first tail arrives, so

$$
\mathbb P(W\mid HH)=0.
$$

After an initial $HT$, a head wins immediately, while a tail leaves $HTT$ and restarts the race. Therefore

$$
\begin{aligned}
\mathbb P(W\mid HT)
&=\frac12\mathbb P(W\mid HTH)
+\frac12\mathbb P(W\mid HTT)\\
&=\frac12+\frac12p.
\end{aligned}
$$

Combining the equations,

$$
p=\frac12\left(\frac12+\frac12p\right)
=\frac14+\frac14p,
$$

which again yields $p=1/3$.

# Remark.

**Equal probabilities in a fixed window do not imply equal winning probabilities.** Each pattern has probability $1/8$ in any specified block of three tosses. However, the race examines overlapping windows and stops at the first occurrence. The patterns interact differently with their partial matches: reaching $HH$ guarantees an eventual $HHT$ win, whereas reaching $HT$ still allows the race to restart. Thus the race is asymmetric, with

$$
\mathbb P(\tau_{HTH}<\tau_{HHT})=\frac13,
\qquad
\mathbb P(\tau_{HHT}<\tau_{HTH})=\frac23.
$$

The related poster [HHT Before HTH -- A Conditional Waiting Time]({% post_url 2026-09-24-hht-before-hth %}) asks for the expected stopping time conditional on $HHT$ winning. This problem instead asks for the probability that $HTH$ wins. The same prefix transitions support both calculations, but the quantities being computed are different.
