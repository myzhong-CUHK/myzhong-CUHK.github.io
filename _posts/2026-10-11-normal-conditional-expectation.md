---
layout: post
title: A Conditional Expectation for Normal Variables
date: 2026-10-11 00:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

$X$ and $Y$ are **jointly normal**, and each has distribution $N(0,1)$, with correlation $\rho \in (-1, 1)$. What is $\mathbb E[X\mid X+Y>0]$?

# Solution.

Let $S=X+Y$. Then $S\sim N(0,\sigma_S^2)$, where $\sigma_S^2=2(1+\rho)>0$. The joint law is symmetric in $X$ and $Y$, so $\mathbb E[X\mid S]=\mathbb E[Y\mid S]$ and

$$
\boxed{\mathbb E[X\mid S]
=\frac12\mathbb E[X+Y\mid S]
=\frac S2.}
$$

Since $\mathbb P(S>0)=1/2$ and $\mathbf1_{\{S>0\}}$ is a function of $S$, the tower property gives

$$
\begin{aligned}
\mathbb E[X\mid S>0]
&=\frac{\mathbb E[X\mathbf1_{\{S>0\}}]}{\mathbb P(S>0)}\\
&=2\mathbb E\!\left[\mathbb E[X\mathbf1_{\{S>0\}}\mid S]\right]\\
&=2\mathbb E\!\left[\mathbb E[X\mid S]\mathbf1_{\{S>0\}}\right]\\
&=2\mathbb E\!\left[\frac S2\mathbf1_{\{S>0\}}\right]\\
&=\mathbb E[S\mathbf1_{\{S>0\}}]\\
&=\frac{1}{\sigma_S\sqrt{2\pi}}
\int_0^\infty s e^{-s^2/(2\sigma_S^2)}\,ds\\
&=\frac{\sigma_S}{\sqrt{2\pi}}
\left[-e^{-s^2/(2\sigma_S^2)}\right]_0^\infty\\
&=\frac{\sigma_S}{\sqrt{2\pi}}
=\boxed{\sqrt{\frac{1+\rho}{\pi}}}.
\end{aligned}
$$
