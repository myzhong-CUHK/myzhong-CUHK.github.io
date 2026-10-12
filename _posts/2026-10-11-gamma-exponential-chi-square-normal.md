---
layout: post
title: Gamma Exponential Chi Square and Normal Distributions
date: 2026-10-11 00:00:00+0800
description: Definitions and derivations linking waiting times, Gaussian squares, and sampling distributions
tags: probability statistics
categories: quant
---

Exponential and chi-square distributions are special cases of the Gamma family. Normal variables enter through their squares: sums of independent squared standard normals are chi-square. Throughout, $\operatorname{Gamma}(\alpha,\lambda)$ uses **shape $\alpha$ and rate $\lambda$**:

$$
\boxed{\operatorname{Exp}(\lambda)=\operatorname{Gamma}(1,\lambda)},
\qquad
\boxed{\chi^2_\nu=\operatorname{Gamma}\!\left(\frac{\nu}{2},\frac12\right)}.
$$

### 1. Gamma distribution and its parameters

For $\alpha,\lambda>0$, a random variable $G\sim\operatorname{Gamma}(\alpha,\lambda)$ has density

$$
f_G(x)=\frac{\lambda^\alpha}{\Gamma(\alpha)}
x^{\alpha-1}e^{-\lambda x},\qquad x>0,
$$

and zero density for $x<0$. The normalizing constant is the **Gamma function**:

$$
\Gamma(\alpha)=\int_0^\infty u^{\alpha-1}e^{-u}\,du,
\qquad
\Gamma(\alpha+1)=\alpha\Gamma(\alpha),
\qquad
\Gamma(1)=1,\quad \Gamma(1/2)=\sqrt\pi.
$$

The recurrence follows by integration by parts, so $\Gamma(m)=(m-1)!$ for positive integers $m$. Substituting $u=\lambda x$ verifies that the density integrates to one.

Under the alternative **shape–scale** convention, the scale is $1/\lambda$, so

$$
f_G(x)=\frac{\lambda^\alpha}{\Gamma(\alpha)} x^{\alpha-1}e^{-\lambda x},
\qquad
\mathbb E[G]=\frac{\alpha}{\lambda},
\qquad
\operatorname{Var}(G)=\frac{\alpha}{\lambda^2}.
$$

Thus a chi-square variable has rate $1/2$, equivalently scale $2$. The second Gamma parameter must always be identified as a rate or a scale.

For any real $p>-\alpha$, the substitution $u=\lambda x$ gives

$$
\begin{aligned}
\mathbb E[G^p]
&=\frac{\lambda^\alpha}{\Gamma(\alpha)}
\int_0^\infty x^{\alpha+p-1}e^{-\lambda x}\,dx\\
&=\frac{\Gamma(\alpha+p)}{\Gamma(\alpha)\lambda^p}.
\end{aligned}
$$

Taking $p=1,2$ and using the Gamma recurrence yields

$$
\mathbb E[G]=\frac{\alpha}{\lambda},
\qquad
\mathbb E[G^2]=\frac{\alpha(\alpha+1)}{\lambda^2},
\qquad
\boxed{\operatorname{Var}(G)=\frac{\alpha}{\lambda^2}}.
$$

Its moment generating function (MGF) is

$$
\begin{aligned}
M_G(t)
&=\frac{\lambda^\alpha}{\Gamma(\alpha)}
\int_0^\infty x^{\alpha-1}e^{-(\lambda-t)x}\,dx\\
&=\left(\frac{\lambda}{\lambda-t}\right)^\alpha,
\qquad t<\lambda.
\end{aligned}
$$

The shape controls the relative dispersion, $\operatorname{sd}(G)/\mathbb E[G]=1/\sqrt\alpha$; the rate controls the scale.

### 2. Scaling and independent sums

For $c>0$, changing variables in the density gives

$$
f_{cG}(x)=\frac1c f_G(x/c)
=\frac{(\lambda/c)^\alpha}{\Gamma(\alpha)}
x^{\alpha-1}e^{-(\lambda/c)x}.
$$

Consequently,

$$
\boxed{cG\sim\operatorname{Gamma}(\alpha,\lambda/c)},
\qquad
\lambda G\sim\operatorname{Gamma}(\alpha,1),
\qquad
\boxed{2\lambda G\sim\chi^2_{2\alpha}}.
$$

If $G_i\sim\operatorname{Gamma}(\alpha_i,\lambda)$ are **independent and have a common rate**, their MGFs multiply:

$$
M_{\sum_iG_i}(t)
=\prod_i\left(\frac{\lambda}{\lambda-t}\right)^{\alpha_i}
=\left(\frac{\lambda}{\lambda-t}\right)^{\sum_i\alpha_i}.
$$

Uniqueness of the MGF therefore gives

$$
\boxed{\sum_iG_i\sim\operatorname{Gamma}\!\left(\sum_i\alpha_i,\lambda\right)}.
$$

With different rates, this product generally does not have a Gamma MGF. Dependence also invalidates the product argument.

### 3. Exponential variables and Poisson waiting times

Setting $\alpha=1$ gives $E\sim\operatorname{Exp}(\lambda)$:

$$
f_E(x)=\lambda e^{-\lambda x}\quad(x>0),
\qquad
\mathbb P(E>x)=e^{-\lambda x}\quad(x\ge0),
\qquad
\mathbb E[E]=\frac1\lambda,\quad
\operatorname{Var}(E)=\frac1{\lambda^2}.
$$

Its **memoryless property** follows directly from the survival function:

$$
\mathbb P(E>s+t\mid E>s)
=\frac{e^{-\lambda(s+t)}}{e^{-\lambda s}}
=e^{-\lambda t}
=\mathbb P(E>t),
\qquad s,t\ge0.
$$

For independent $E_1,\ldots,E_m\sim\operatorname{Exp}(\lambda)$, Gamma additivity gives

$$
\boxed{T_m=\sum_{i=1}^mE_i\sim\operatorname{Gamma}(m,\lambda)},
\qquad
\mathbb E[T_m]=\frac m\lambda,
\qquad
\operatorname{Var}(T_m)=\frac m{\lambda^2}.
$$

The Gamma distribution with positive integer shape $m$ is also called an **Erlang distribution**. In a homogeneous Poisson process $N(t)$ of rate $\lambda$, the interarrival times are independent $\operatorname{Exp}(\lambda)$ variables, so $T_m$ is the time of the $m$th arrival. Equivalently,

$$
\mathbb P(T_m>t)
=\mathbb P(N(t)\le m-1)
=e^{-\lambda t}\sum_{k=0}^{m-1}\frac{(\lambda t)^k}{k!},
\qquad t\ge0.
$$

Differentiating the survival function recovers

$$
f_{T_m}(t)
=-\frac{d}{dt}\mathbb P(T_m>t)
=\frac{\lambda^m}{(m-1)!}t^{m-1}e^{-\lambda t},
\qquad t>0.
$$

For noninteger shape, the Gamma density still makes sense, but there is no literal “$\alpha$th arrival” interpretation. Among Gamma distributions, only shape $1$ is memoryless.

### 4. Normal squares and chi-square distributions

For $Z\sim N(0, 1)$, 

$$
\boxed{Z^2\sim\chi^2_1=\operatorname{Gamma}(1/2,1/2)}.
$$

For independent $Z_1,\ldots,Z_\nu\sim N(0,1)$ and integer $\nu\ge1$, Gamma additivity gives

$$
\boxed{
Q=\sum_{i=1}^{\nu}Z_i^2
\sim\chi^2_\nu
=\operatorname{Gamma}\!\left(\frac\nu2,\frac12\right).
}
$$
