---
layout: post
title: A Conditional Expectation for Normal Variables
date: 2026-10-11 00:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

X and Y each have distribution $N(0,1)$, with correlation $\rho$. What is $\mathbb E[X\mid X+Y>0]$?

# Solution.

### 1. The missing assumption

The normal marginals and correlation alone do not determine the answer. To obtain the usual formula, assume additionally that $X$ and $Y$ are **jointly normal**. First consider $-1<\rho\leq1$, and put

$$
S=X+Y,
\qquad
S\sim N(0,\sigma_S^2),
\qquad
\sigma_S^2=2(1+\rho)>0.
$$

### 2. Condition on the sum

Write $X=S/2+R$, where $R=(X-Y)/2$. Then

$$
\mathbb E[R]=0,
\qquad
\operatorname{Cov}(R,S)
=\frac12\operatorname{Cov}(X-Y,X+Y)
=\frac12\bigl(\operatorname{Var}(X)-\operatorname{Var}(Y)\bigr)=0.
$$

Since $R$ and $S$ are jointly normal, zero covariance implies independence. This also covers $\rho=1$, when $R=0$ almost surely. Consequently,

$$
\boxed{\mathbb E[X\mid S]=\frac S2.}
$$

### 3. Normalize the truncated density

By symmetry, $\mathbb P(S>0)=1/2$. Conditioning on $S>0$ restricts the density to the positive half-line and divides by the probability of that half-line:

$$
f_{S\mid S>0}(s)
=\frac{f_S(s)}{\mathbb P(S>0)}
=\frac{2}{\sigma_S\sqrt{2\pi}}
e^{-s^2/(2\sigma_S^2)},
\qquad s>0.
$$

Thus the conditional mean is

$$
\begin{aligned}
\mathbb E[S\mid S>0]
&=\int_0^\infty s\frac{f_S(s)}{\mathbb P(S>0)}\,ds\\
&=\frac{2}{\sigma_S\sqrt{2\pi}}
\int_0^\infty s e^{-s^2/(2\sigma_S^2)}\,ds\\
&=\frac{2\sigma_S}{\sqrt{2\pi}}
\left[-e^{-s^2/(2\sigma_S^2)}\right]_0^\infty
=\sigma_S\sqrt{\frac2\pi}.
\end{aligned}
$$

Without the denominator $\mathbb P(S>0)$, the integral would give $\mathbb E[S\mathbf1_{\{S>0\}}]$, which is half the conditional mean. Averaging $\mathbb E[X\mid S]=S/2$ over $S>0$ now gives

$$
\boxed{
\mathbb E[X\mid X+Y>0]
=\frac12\mathbb E[S\mid S>0]
=\sqrt{\frac{1+\rho}{\pi}},
\qquad -1<\rho\leq1.
}
$$

If $\rho=-1$, then $\operatorname{Var}(X+Y)=0$, so $X+Y=0$ almost surely. The conditioning event has probability zero, and the requested conditional expectation is undefined.

### 4. Why normal marginals are insufficient

Let $X\sim N(0,1)$, let $\varepsilon$ be an independent fair sign taking values $\pm1$, and set $Y=\varepsilon X$. Symmetry gives $Y\sim N(0,1)$, while

$$
\operatorname{Corr}(X,Y)
=\mathbb E[\varepsilon X^2]
=\mathbb E[\varepsilon]\mathbb E[X^2]=0.
$$

Here $X+Y>0$ occurs exactly when $\varepsilon=1$ and $X>0$, so

$$
\mathbb E[X\mid X+Y>0]
=\mathbb E[X\mid X>0]
=\sqrt{\frac2\pi}.
$$

Independent standard normals have the same marginals and correlation $0$, but give $1/\sqrt\pi$. Thus the joint distribution is needed to determine the answer.
