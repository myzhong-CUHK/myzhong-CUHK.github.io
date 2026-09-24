---
layout: post
title: HHT Before HTH -- A Conditional Waiting Time
date: 2026-09-24 12:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

A fair coin is tossed independently until either $HHT$ or $HTH$ appears as three consecutive outcomes. Conditional on $HHT$ appearing first, what is the expected number of tosses?

# Solution.

Let $T$ be the total number of tosses until either pattern first appears, and let $W$ be the event that $HHT$ appears before $HTH$. We seek $\mathbb E[T\mid W]$.

Record only the longest suffix of the observed tosses that matches an unfinished beginning of either target. The possible suffixes are $\varnothing,H,HH,HT$. For example, $HHH$ is recorded as $HH$, while $HTT$ is recorded as $\varnothing$. For a current suffix $s$, write $\mathbb P_s,\mathbb E_s$ for probability and expectation starting from that suffix, and let $\tau$ count the additional tosses until one target is completed. From $\varnothing$, $\tau=T$.

### 1. The probability that HHT appears first

Define

$$
q_s:=\mathbb P_s(W),
\qquad s\in\{\varnothing,H,HH,HT\}.
$$

Conditioning on the next toss gives

$$
\begin{aligned}
q_\varnothing&=\tfrac12q_\varnothing+\tfrac12q_H,\\
q_H&=\tfrac12q_{HH}+\tfrac12q_{HT},\\
q_{HH}&=\tfrac12q_{HH}+\tfrac12,\\
q_{HT}&=\tfrac12q_\varnothing.
\end{aligned}
$$

In the third equation, a tail completes $HHT$; in the fourth, a head completes $HTH$ and contributes zero. Solving,

$$
q_{HH}=1,\qquad
q_H=q_\varnothing,\qquad
q_{HT}=\frac12q_\varnothing,
$$

and hence

$$
q_\varnothing=\frac12+\frac14q_\varnothing.
$$

Therefore,

$$
\boxed{
q_\varnothing=q_H=\frac23,\qquad
q_{HH}=1,\qquad q_{HT}=\frac13.
}
$$

### 2. The first moment restricted to successful outcomes

Define

$$
m_s:=\mathbb E_s[\tau\,\mathbf1_W].
$$

Its relation to the conditional expectation is

$$
m_s=q_s\,\mathbb E_s[\tau\mid W],
\qquad q_s=\mathbb P_s(W).
$$

Starting from suffix $s$, let $\tau'$ be the number of tosses still needed after the next toss, with $\tau'=0$ if that toss completes a target. Then

$$
\tau=1+\tau'.
$$

Consequently,

$$
\begin{aligned}
m_s
&=\mathbb E_s[(1+\tau')\mathbf1_W]\\
&=\underbrace{\mathbb E_s[\mathbf1_W]}_{q_s}
+\mathbb E_s[\tau'\mathbf1_W].
\end{aligned}
$$

Although the next toss certainly takes place, it contributes $1$ to $\tau\mathbf1_W$ only when $W$ occurs. Its expected contribution is therefore the success probability $q_s$.

Let $P_{sj}$ be the probability that the next toss leaves the unfinished suffix $j\in\{\varnothing,H,HH,HT\}$. Conditional on this outcome, the remaining weighted expectation is $m_j$; if a target is completed, there is no remaining contribution. Conditioning on the next suffix gives

$$
m_s=q_s+\sum_jP_{sj}m_j.
$$

Using the next-toss probabilities and $q_\varnothing=q_H=2/3$, $q_{HH}=1$, $q_{HT}=1/3$, we obtain

$$
\begin{aligned}
m_\varnothing&=\tfrac23+\tfrac12m_\varnothing+\tfrac12m_H,\\
m_H&=\tfrac23+\tfrac12m_{HH}+\tfrac12m_{HT},\\
m_{HH}&=1+\tfrac12m_{HH},\\
m_{HT}&=\tfrac13+\tfrac12m_\varnothing.
\end{aligned}
$$

Solving these equations gives

$$
m_\varnothing=\frac{38}{9}.
$$

Finally, by the definition of conditional expectation,

$$
\boxed{
\mathbb E[T\mid W]
=\frac{\mathbb E[T\mathbf1_W]}{\mathbb P(W)}
=\frac{m_\varnothing}{q_\varnothing}
=\frac{38/9}{2/3}
=\frac{19}{3}.
}
$$
