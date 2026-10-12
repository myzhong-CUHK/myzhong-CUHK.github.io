---
layout: post
title: A Mathematical Review of Linear Regression
date: 2026-10-11 00:00:00+0800
description: Least squares, projection geometry, inference, and estimability
tags: statistics regression
categories: quant
---

### 1. Model, notation, and assumptions

With $n$ observations and $d$ coefficients, including the intercept, write

$$
\mathbf y=X\boldsymbol\beta+\boldsymbol\varepsilon,
\quad
X=[\,\mathbf 1_n\ \ \widetilde X\,]\in\mathbb R^{n\times d},
\quad
\boldsymbol\beta=
\begin{pmatrix}\beta_0\\\widetilde{\boldsymbol\beta}\end{pmatrix},
$$

with $y_i=\beta_0+\widetilde{\mathbf x}_i^{\top}\widetilde{\boldsymbol\beta}+\varepsilon_i$, where the predictor vector $\widetilde{\mathbf x}_i\in\mathbb R^{d-1}$, and the $i$-th row of $\widetilde X$ is $\widetilde{\mathbf x}_i^{\top}$. Unless stated otherwise, assume $\operatorname{rank}(X)=d<n$. Least-squares algebra needs no further assumptions. The classical moment assumptions are

$$
\mathbb E[\boldsymbol\varepsilon\mid X]=\mathbf0,
\quad
\operatorname{Cov}(\boldsymbol\varepsilon\mid X)=\sigma^2I_n,
\quad \sigma^2>0.
$$

Exact finite-sample $t$ and $F$ inference uses the stronger Gaussian assumption

$$
\boldsymbol\varepsilon\mid X\sim N(\mathbf0,\sigma^2I_n).
$$

### 2. OLS and projection geometry

Ordinary least squares (OLS) minimizes $Q(\mathbf b)=\|\mathbf y-X\mathbf b\|_2^2$. Its first-order condition gives

$$
\nabla Q(\mathbf b)=-2X^{\top}\mathbf y+2X^{\top}X\mathbf b.
$$

Hence, as $X$ has full column rank and $X^\top X \succ 0$, we have

$$
\boxed{\widehat{\boldsymbol\beta}=(X^{\top}X)^{-1}X^{\top}\mathbf y},
$$

Denote $H=X(X^{\top}X)^{-1}X^{\top}$, then we have $\widehat{\mathbf y}=H\mathbf y$, and residual $\mathbf e=(I_n-H)\mathbf y$. Here, $H$ is the orthogonal projection matrix onto the **column space** $\mathcal C(X)\subseteq\mathbb R^n$. The residual lies in $\mathcal C(X)^\perp=\ker(X^{\top})$, i.e., $X^{\top}\mathbf e=\mathbf0$. 
The Pythagorean identity gives both the minimization property and a useful expansion:

$$
Q(\mathbf b)
=\underbrace{\|\mathbf e\|^2}_{\mathrm{SSE}}
+(\mathbf b-\widehat{\boldsymbol\beta})^{\top}
X^{\top}X(\mathbf b-\widehat{\boldsymbol\beta}).
$$

### 3. The intercept, sums of squares, and $R^2$

The intercept FOC gives

$$
0=\left.\frac{\partial Q}{\partial\beta_0}\right|_{\widehat{\boldsymbol\beta}}
=-2\sum_{i=1}^n
\left(y_i-\widehat\beta_0-\widetilde{\mathbf x}_i^{\top}\widehat{\widetilde{\boldsymbol\beta}}\right)
=-2\sum_{i=1}^n e_i.
$$

Consequently, $\sum_i e_i=0$. Define **SSE (Sum of Squared Errors)**, **TSS (Total Sum of Squares)**, and **SSR (Regression Sum of Squares)** by

$$
\mathrm{SSE}=\sum_i(y_i-\widehat y_i)^2,
\quad
\mathrm{TSS}=\sum_i(y_i-\bar y)^2,
\quad
\mathrm{SSR}=\sum_i(\widehat y_i-\bar y)^2.
$$

Since $\widehat{\mathbf y}-\bar y\mathbf1_n\in\mathcal C(X)$ and $\mathbf e\perp\mathcal C(X)$,

$$
\mathbf y-\bar y\mathbf1_n
=(\widehat{\mathbf y}-\bar y\mathbf1_n)+\mathbf e
\quad\Longrightarrow\quad
\boxed{\mathrm{TSS}=\mathrm{SSR}+\mathrm{SSE}}.
$$

Define

$$
R^2=1-\frac{\mathrm{SSE}}{\mathrm{TSS}}
=\frac{\mathrm{SSR}}{\mathrm{TSS}}.
$$

### 4. Sampling covariance and residual degrees of freedom

Substitution of the model yields

$$
\begin{aligned}
\widehat{\boldsymbol\beta}-\boldsymbol\beta
&=(X^{\top}X)^{-1}X^{\top}\boldsymbol\varepsilon,\\
\mathbb E[\widehat{\boldsymbol\beta}\mid X]&=\boldsymbol\beta,\\
\operatorname{Cov}(\widehat{\boldsymbol\beta}\mid X)
&=(X^{\top}X)^{-1}X^{\top}(\sigma^2I_n)X(X^{\top}X)^{-1}
=\sigma^2(X^{\top}X)^{-1}.
\end{aligned}
$$

The residual satisfies

$$
\begin{aligned}
\mathbf e
=\mathbf y-\widehat{\mathbf y}
=(I_n-H)\mathbf y
=(I_n-H)X\boldsymbol\beta+(I_n-H)\boldsymbol\varepsilon
=(I_n-H)\boldsymbol\varepsilon,
\end{aligned}
$$

which yields

$$
\mathbb E[\mathrm{SSE}\mid X]
=\mathbb E[\boldsymbol\varepsilon^{\top}(I_n-H)\boldsymbol\varepsilon\mid X]
=\sigma^2(n-d).
$$

Thus fitting a $d$-dimensional mean leaves $n-d$ residual degrees of freedom. Then, the estimator of $\sigma^2$ is given by

$$
\boxed{\widehat{\sigma}^2=\frac{\mathrm{SSE}}{n-d}}.
$$

Under the moment assumptions, OLS is also the best linear unbiased estimator (Gauss–Markov).

### 5. Gaussian independence and coefficient inference

#### 5.1 Two independence lemmas

Let $\mathbf W\sim N_m(\boldsymbol\mu,\Sigma)$ with $\Sigma \succ 0$.

**Lemma 1 (linear and quadratic forms).** If $A\in\mathbb R^{m\times m}$ is symmetric and $B\in\mathbb R^{k\times m}$, then

$$
\boxed{
B\mathbf W\ \perp\!\!\!\perp\ \mathbf W^{\top}A\mathbf W
\quad\Longleftrightarrow\quad B\Sigma A=0.
}
$$

**Lemma 2 (two quadratic forms, Craig's theorem).** If $A,B\in\mathbb R^{m\times m}$ are symmetric, then

$$
\boxed{
\mathbf W^{\top}A\mathbf W\ \perp\!\!\!\perp\
\mathbf W^{\top}B\mathbf W
\quad\Longleftrightarrow\quad A\Sigma B=0.
}
$$

If $\Sigma=\sigma^2I_m$ and $A$ is an orthogonal projection of rank $r$, then

$$
\frac{\mathbf W^{\top}A\mathbf W}{\sigma^2}
\sim\chi^2(r,s),
\quad
s=\frac{\boldsymbol\mu^{\top}A\boldsymbol\mu}{\sigma^2}
=\frac{\|A\boldsymbol\mu\|^2}{\sigma^2}.
$$

This is the central $\chi^2(r)$ distribution when $A\boldsymbol\mu=0$.

#### 5.2 Applying Lemma 1 to coefficient tests

Under Gaussian errors, conditional on $X$, with $\Sigma=\sigma^2I_n$,

$$
\widehat{\boldsymbol\beta}\sim N(\boldsymbol\beta,\sigma^2(X^{\top}X)^{-1}),
\quad
\frac{\mathrm{SSE}}{\sigma^2}\sim\chi^2(n-d).
$$

Note that $\widehat{\boldsymbol\beta} = (X^{\top}X)^{-1}X^{\top} \mathbf y$ and $\mathrm{SSE} = \mathbf y^{\top}(I_n-H)\mathbf y$, together with 

$$
\bigl[(X^{\top}X)^{-1}X^{\top}\bigr]\Sigma(I_n-H)
=\sigma^2(X^{\top}X)^{-1}\bigl[X^{\top}-X^{\top}H\bigr]=0.
$$

Thus Lemma 1 and $\widehat{\sigma}^2=\mathrm{SSE}/(n-d)$ give $\widehat{\boldsymbol\beta}\ \perp\!\!\!\perp\ \mathrm{SSE}$ and $\widehat\beta_j\ \perp\!\!\!\perp\ \widehat{\sigma}^2$. Under $H_0:\beta_j=0$, we have

$$
\boxed{t_j=\frac{\widehat\beta_j}{\widehat{\sigma}\sqrt{\bigl[(X^{\top}X)^{-1}\bigr]_{jj}}}\sim t(n-d)\quad\text{under }H_0}.
$$

### 6. Testing every coefficient versus testing every slope

Let $J=\mathbf1_n\mathbf1_n^{\top}/n$. We have

$$
\mathrm{SSR}=\mathbf y^{\top}(H-J)\mathbf y,
\quad
\mathrm{SSE}=\mathbf y^{\top}(I_n-H)\mathbf y.
$$

By $(H-J)(I_n-H)=0.$, Lemma 2 gives

$$
\boxed{\mathrm{SSR}\ \perp\!\!\!\perp\ \mathrm{SSE}}.
$$

Similarly, by Lemma 2 and $H(I_n-H)=0$,

$$
\|\widehat{\mathbf y}\|^2=\mathbf y^{\top}H\mathbf y
\ \perp\!\!\!\perp\ \mathrm{SSE}.
$$

Under Gaussian errors and $H_0:\boldsymbol\beta=\mathbf0$ (including the intercept), $\mathbf y=\boldsymbol\varepsilon\sim N(\mathbf0,\sigma^2I_n)$ conditional on $X$. Since $H$ and $I_n-H$ are projections of ranks $d$ and $n-d$,

$$
\frac{\|\widehat{\mathbf y}\|^2}{\sigma^2}
=\frac{\mathbf y^{\top}H\mathbf y}{\sigma^2}\sim\chi^2(d),
\quad
\frac{\mathrm{SSE}}{\sigma^2}\sim\chi^2(n-d).
$$

These quadratic forms are independent, as shown above. Dividing each by its degrees of freedom gives

$$
\begin{aligned}
F_{\mathrm{all}}
&=\frac{\bigl(\|\widehat{\mathbf y}\|^2/\sigma^2\bigr)/d}
{\bigl(\mathrm{SSE}/\sigma^2\bigr)/(n-d)}\\
&=\frac{\|\widehat{\mathbf y}\|^2}{d\,\widehat{\sigma}^2}
=\frac{\widehat{\boldsymbol\beta}^{\top}X^{\top}X\widehat{\boldsymbol\beta}}{d\,\widehat{\sigma}^2}
\sim F_{d,n-d}\quad\text{under }H_0.
\end{aligned}
$$

As for $H_0:\widetilde{\boldsymbol\beta}=\mathbf0$, with $d\ge2$, $(H-J)X\boldsymbol\beta=(H-J)\beta_0\mathbf1_n=0$. Since $H-J$ has rank $d-1$, $\mathrm{SSR}/\sigma^2\sim\chi^2(d-1)$. The restricted fit is $\bar y\mathbf1_n$, with residual sum of squares $\mathrm{TSS}$. Thus

$$
\boxed{
F_{\mathrm{slopes}}
=\frac{\mathrm{SSR}/(d-1)}{\mathrm{SSE}/(n-d)}
=\frac{R^2/(d-1)}{(1-R^2)/(n-d)}
\sim F_{d-1,n-d}\quad\text{under }H_0.
}
$$

The distinction is $\|\widehat{\mathbf y}\|^2=\mathrm{SSR}+n\bar y^2$: the full-vector test also includes the fitted mean level.

### 7. Rank deficiency, pseudoinverses, and estimability

Let $X\in\mathbb R^{n\times d}$ have rank $r<d$, allowing $d\ge n$. Then $X^{\top}X$ is singular, but least squares still has minimizers.

#### 7.1 Definition of the generalized inverse

A **generalized inverse** $G\in\mathbb R^{d\times n}$ satisfies $XGX=X$ and need not be unique. Here $X^+$ denotes the unique **Moore–Penrose inverse**, characterized by

$$
\begin{gathered}
XX^+X=X,\qquad X^+XX^+=X^+,\\
(XX^+)^{\top}=XX^+,\qquad (X^+X)^{\top}=X^+X.
\end{gathered}
$$

#### 7.2 Properties of the Moore–Penrose inverse
The Moore–Penrose inverse satisfies 

$$
X^{\top}(I_n-XX^+)=0,
\qquad
X^+\mathbf y\in\mathcal C(X^{\top})=\ker(X)^\perp.
$$

A useful identity is $(X^{\top}X)^+=X^+(X^+)^{\top}$. Together with the defining equations, it gives

$$
\begin{aligned}
(X^{\top}X)^+X^{\top}
&=X^+(X^+)^{\top}X^{\top}=X^+(XX^+)^{\top}
=X^+XX^+
=X^+.
\end{aligned}
$$

For full column rank, this reduces to $X^+=(X^{\top}X)^{-1}X^{\top}$.

#### 7.3 Estimation when $X$ is not of full column rank

The Moore–Penrose estimate is

$$
\boxed{\widehat{\boldsymbol\beta}_{\min}
=X^+\mathbf y=(X^{\top}X)^+X^{\top}\mathbf y},
$$

which solves the normal equations. Since $\ker(X^{\top}X)=\ker(X)$, **all** OLS solutions are

$$
\boxed{\widehat{\boldsymbol\beta}=X^+\mathbf y+\mathbf h,
\qquad \mathbf h\in\ker(X)}.
$$

By $X^+\mathbf y\perp\ker(X)$,

$$
\|\widehat{\boldsymbol\beta}\|^2
=\|X^+\mathbf y\|^2+\|\mathbf h\|^2
\ge\|X^+\mathbf y\|^2,
$$

with equality only for $\mathbf h=\mathbf0$. Thus $\widehat{\boldsymbol\beta}_{\min}$ is the unique OLS solution of minimum Euclidean norm. Every OLS solution has the same fitted values and residuals:

$$
\widehat{\mathbf y}=XX^+\mathbf y,\qquad
\mathbf e=(I_n-XX^+)\mathbf y,\qquad
\mathrm{SSE}=\|\mathbf e\|^2.
$$

Under the classical moment assumptions,

$$
\begin{aligned}
\mathbb E[\widehat{\boldsymbol\beta}_{\min}\mid X]
&=X^+X\boldsymbol\beta,\\
\operatorname{Cov}(\widehat{\boldsymbol\beta}_{\min}\mid X)
&=\sigma^2X^+(X^+)^{\top}=\sigma^2(X^{\top}X)^+.
\end{aligned}
$$

Hence $\widehat{\boldsymbol\beta}_{\min}$ is unbiased for the row-space component of $\boldsymbol\beta$; it is unbiased for $\boldsymbol\beta$ itself exactly when $\boldsymbol\beta\in\mathcal C(X^{\top})$. Since $I_n-XX^+$ has rank $n-r$,

$$
\mathbb E[\mathrm{SSE}\mid X]
=\sigma^2\operatorname{tr}(I_n-XX^+)=\sigma^2(n-r),
\qquad
\boxed{\widehat{\sigma}^2=\frac{\mathrm{SSE}}{n-r}}\quad(n>r).
$$

The residual degrees of freedom are $n-r$. If $r=n$, this variance estimate is unavailable.

#### 7.4 Which quantities are estimable?

A linear functional $L=\mathbf a^{\top}\boldsymbol\beta$ is **estimable** if some linear estimator $\mathbf u^{\top}\mathbf y$ is unbiased. The criterion is

$$
\boxed{
\mathbf a^{\top}\boldsymbol\beta\text{ is estimable}
\iff \mathbf a\perp\ker(X)
\iff \mathbf a\in\mathcal C(X^{\top}).
}
$$

Indeed, $\mathbb E[\mathbf u^{\top}\mathbf y\mid X]=\mathbf u^{\top}X\boldsymbol\beta$ equals $\mathbf a^{\top}\boldsymbol\beta$ for every $\boldsymbol\beta$ exactly when $X^{\top}\mathbf u=\mathbf a$. Equivalently, the value of $L$ must be unchanged when any $\mathbf h\in\ker(X)$ is added to $\boldsymbol\beta$.

For estimable $\mathbf a$, every OLS solution gives the same estimate because $\mathbf a^{\top}\mathbf h=0$. In particular,

$$
\begin{gathered}
\widehat L=\mathbf a^{\top}\widehat{\boldsymbol\beta}_{\min},
\quad \mathbb E[\widehat L\mid X]=L,\\
\operatorname{Var}(\widehat L\mid X)=\sigma^2\mathbf a^{\top}(X^{\top}X)^+\mathbf a,
\quad
\widehat{\operatorname{se}}(\widehat L)
=\widehat{\sigma}\sqrt{\mathbf a^{\top}(X^{\top}X)^+\mathbf a}.
\end{gathered}
$$

The exact test of $H_0:L=L_0$ is

$$
\boxed{
t=\frac{\widehat L-L_0}
{\widehat{\sigma}\sqrt{\mathbf a^{\top}(X^{\top}X)^+\mathbf a}}
\sim t(n-r)\quad\text{under }H_0.
}
$$

The independence follows from Lemma 1 and

$$
\left(\mathbf a^{\top}X^+\right)\Sigma \left(I_n-XX^+\right)
=\sigma^2\mathbf a^{\top}(X^+-X^+XX^+)=0.
$$

Hence $\widehat L\perp\!\!\!\perp\mathrm{SSE}$. The residual projection has rank $n-r$ and $\mathrm{SSE}/\sigma^2\sim\chi^2(n-r)$. 

#### 7.5 Example: a duplicated block of predictors

Let $Z\in\mathbb R^{n\times p}$ satisfy $\operatorname{rank}([\,\mathbf1_n\ Z\,])=p+1$, and set $X=[\,\mathbf1_n\ Z\ Z\,]\in\mathbb R^{n\times(2p+1)}$. For coefficient blocks $\boldsymbol\beta_1,\boldsymbol\beta_2\in\mathbb R^p$,

$$
\boldsymbol\beta=
\begin{pmatrix}\beta_0\\\boldsymbol\beta_1\\\boldsymbol\beta_2\end{pmatrix},
\qquad
X\boldsymbol\beta=\beta_0\mathbf1_n+Z(\boldsymbol\beta_1+\boldsymbol\beta_2).
$$

Let $(\widehat\alpha,\widehat{\mathbf b})$ be the unique OLS fit of the reduced model:

$$
(\widehat\alpha,\widehat{\mathbf b})
=\underset{\alpha\in\mathbb R,\,\mathbf b\in\mathbb R^p}{\operatorname{argmin}}
\|\mathbf y-\alpha\mathbf1_n-Z\mathbf b\|^2.
$$

Since $\ker(X)=\{(0,\mathbf c^{\top},-\mathbf c^{\top})^{\top}:\mathbf c\in\mathbb R^p\}$, all OLS solutions and the minimum-norm choice are

$$
\widehat{\boldsymbol\beta}
=\begin{pmatrix}\widehat\alpha\\\widehat{\mathbf b}/2+\mathbf c\\\widehat{\mathbf b}/2-\mathbf c\end{pmatrix},
\quad \mathbf c\in\mathbb R^p,
\qquad
\boxed{\widehat{\boldsymbol\beta}_{\min}
=\begin{pmatrix}\widehat\alpha\\\widehat{\mathbf b}/2\\\widehat{\mathbf b}/2\end{pmatrix}}.
$$

The equal split follows from

$$
\|\widehat{\mathbf b}/2+\mathbf c\|^2
+\|\widehat{\mathbf b}/2-\mathbf c\|^2
=\tfrac12\|\widehat{\mathbf b}\|^2+2\|\mathbf c\|^2.
$$

The intercept $\beta_0$ and block sum $\boldsymbol\beta_1+\boldsymbol\beta_2$ are estimable; the individual blocks are not. The equal split is a minimum-norm convention. Here $r=p+1$, so $\widehat{\sigma}^2=\mathrm{SSE}/(n-p-1)$ when $n>p+1$.

### 8. Regularization

Ridge and lasso change the optimization problem by penalizing coefficients. With an unpenalized intercept and $D=\operatorname{diag}(0,1,\ldots,1)$, ridge solves

$$
\min_{\mathbf b}\left\{\|\mathbf y-X\mathbf b\|^2+\lambda\mathbf b^{\top}D\mathbf b\right\},
\quad
\widehat{\boldsymbol\beta}_{\lambda}
=(X^{\top}X+\lambda D)^{-1}X^{\top}\mathbf y,
\quad \lambda>0.
$$

Penalizing all slopes makes this inverse well defined even when predictor columns are linearly dependent. Ridge trades bias for reduced variance; its fitted-value matrix is generally not an orthogonal projection. Lasso replaces the quadratic penalty by $\lambda\sum_{j=1}^{d-1}|b_j|$, which can set slopes exactly to zero and can have nonunique coefficients under collinearity. Penalties depend on predictor scales, so standardization and the convention for $\lambda$ matter.
