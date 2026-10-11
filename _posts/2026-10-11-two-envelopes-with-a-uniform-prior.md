---
layout: post
title: Two Envelopes with a Uniform Prior
date: 2026-10-11 12:01:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

Let $X\sim\operatorname{Unif}(0,100)$. Two envelopes contain $X$ dollars and $2X$ dollars. You choose an envelope, and open it to observe its amount. You may then keep it or switch to the other envelope. What strategy maximizes the probability of ending with the larger amount, and what is this probability? Does the same strategy maximize the expected amount received?

# Solution.

Write $Y$ for the observed amount and $Z$ for the amount in the other envelope. Let $S$ be the event that the selected envelope is the smaller one, so $Y=X$ and $Z=2X$, and let $L$ be the event that it is the larger one, so $Y=2X$ and $Z=X$. Before observing $Y$, both events have probability $1/2$.

### 1. Update the probabilities after seeing the amount

If $100<Y<200$, the selected envelope must be the larger one: the smaller amount $X$ never exceeds $100$. Keeping it wins with certainty.

If $0<Y<100$, either envelope could have been selected. The conditional densities are

$$
f_{Y\mid S}(y)=\frac1{100},\qquad
f_{Y\mid L}(y)=\frac1{200},
\qquad 0<y<100.
$$

The second density is smaller because $Y=2X$ spreads the same probability mass over an interval twice as long. Since $Y$ is continuous, we use these densities in Bayes' formula:

$$
\mathbb P(S\mid Y=y)
=\frac{\frac12\cdot\frac1{100}}
 {\frac12\cdot\frac1{100}+\frac12\cdot\frac1{200}}
=\frac23,
\qquad
\mathbb P(L\mid Y=y)=\frac13.
$$

Equivalently, observing an amount in a short interval $[y,y+\mathrm{d}y]$ corresponds to an interval of width $\mathrm{d}y$ for $X$ if the smaller envelope was selected, but only width $\mathrm{d}y/2$ if the larger envelope was selected. The two explanations therefore have probability ratio $2:1$.

### 2. Choose the action with the higher winning probability

For $0<y<100$, switching wins exactly when the selected envelope is the smaller one, with conditional probability $2/3$; keeping wins with probability $1/3$. For $100<y<200$, keeping wins with certainty. Thus an optimal strategy is

$$
\boxed{
\text{Switch if }Y\leq100;\qquad
\text{keep if }Y>100.
}
$$

The observation $Y=100$ has probability zero, so the action at this boundary does not affect the overall result. Comparing the two actions at each observed amount establishes optimality; randomizing between them cannot improve the conditional winning probability.

To calculate the overall winning probability, condition on which envelope was initially selected. If we selected $X$, then $Y=X\leq100$ and we always switch to $2X$. If we selected $2X$, we keep the larger envelope exactly when $2X>100$, or $X>50$. Therefore

$$
\boxed{
\mathbb P(\text{finish with }2X)
=\frac12\cdot1+\frac12\mathbb P(X>50)
=\frac12+\frac12\cdot\frac12
=\frac34.
}
$$

### 3. Maximize the expected amount

For $0<y<100$, the other envelope contains $2y$ with posterior probability $2/3$ and $y/2$ with probability $1/3$. Hence

$$
\mathbb E[Z\mid Y=y]
=\frac23(2y)+\frac13\left(\frac y2\right)
=\frac32y>y.
$$

For $100<y<200$, the other envelope certainly contains $y/2<y$. Thus the same strategy also maximizes expected dollars received.

Let $V$ be the final amount under this strategy. Conditional on initially selecting the smaller envelope, $V=2X$. Conditional on initially selecting the larger envelope, $V=X$ when $X\leq50$ and $V=2X$ when $X>50$. Consequently,

$$
\begin{aligned}
\mathbb E[V]
&=\frac12\mathbb E[2X]
 +\frac12\left(
 \int_0^{50}\frac{x}{100}\,\mathrm{d}x
 +\int_{50}^{100}\frac{2x}{100}\,\mathrm{d}x
 \right)\\
&=50+\frac12(12.5+75)
=\boxed{93.75\text{ dollars}}.
\end{aligned}
$$

For comparison, always keeping or always switching gives expected amount $\frac12\mathbb E[X]+\frac12\mathbb E[2X]=75$ dollars. Observing the amount and acting on it raises the expectation by $18.75$ dollars.
