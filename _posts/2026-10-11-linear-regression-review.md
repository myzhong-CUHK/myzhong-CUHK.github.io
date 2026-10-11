---
layout: post
title: A Mathematical Review of Linear Regression
date: 2026-10-11 00:00:00+0800
description: Least squares, projection geometry, inference, and estimability
tags: statistics regression
categories: quant
---

Linear regression has three distinct layers: least squares is an optimization problem, projection explains its geometry, and assumptions on the errors justify statistical inference.

### 1. Model, notation, and assumptions

With $n$ observations and $d$ coefficients, including the intercept, write

$$
\mathbf y=X\boldsymbol\beta+\boldsymbol\varepsilon,
\qquad
X=[\,\mathbf 1_n\ \ \widetilde X\,]\in\mathbb R^{n\times d},
\qquad
\boldsymbol\beta=
\begin{pmatrix}\beta_0\\\widetilde{\boldsymbol\beta}\end{pmatrix}
=\bigl(\beta_0,\widetilde{\boldsymbol\beta}^{\top}\bigr)^{\top}.
$$

The predictor vector $\widetilde{\mathbf x}_i\in\mathbb R^{d-1}$ is a **column vector**; the $i$th row of $\widetilde X$ is $\widetilde{\mathbf x}_i^{\top}$. Thus

$$
y_i=\beta_0+\widetilde{\mathbf x}_i^{\top}\widetilde{\boldsymbol\beta}+\varepsilon_i.
$$

Unless stated otherwise, assume $\operatorname{rank}(X)=d<n$ and condition on $X$. Least-squares algebra needs no distributional assumptions. The classical moment assumptions are

$$
\mathbb E[\boldsymbol\varepsilon\mid X]=\mathbf0,
\qquad
\operatorname{Cov}(\boldsymbol\varepsilon\mid X)=\sigma^2I_n,
\qquad \sigma^2>0.
$$

These give unbiasedness and the usual sampling covariance. Equal variances and zero correlations alone do not imply independence. Exact finite-sample $t$ and $F$ inference uses the stronger Gaussian assumption

$$
\boldsymbol\varepsilon\mid X\sim N(\mathbf0,\sigma^2I_n).
$$

### 2. OLS and projection geometry

Ordinary least squares (OLS) minimizes $Q(\mathbf b)=\|\mathbf y-X\mathbf b\|_2^2$. Its first-order condition (FOC) gives

$$
\nabla Q(\mathbf b)=-2X^{\top}\mathbf y+2X^{\top}X\mathbf b,
\qquad
X^{\top}X\widehat{\boldsymbol\beta}=X^{\top}\mathbf y.
$$

Full column rank makes $X^{\top}X$ positive definite because $\mathbf a^{\top}X^{\top}X\mathbf a=\|X\mathbf a\|^2>0$ for every nonzero $\mathbf a$. Hence

$$
\boxed{\widehat{\boldsymbol\beta}=(X^{\top}X)^{-1}X^{\top}\mathbf y},
\qquad
\widehat{\mathbf y}=H\mathbf y,
\qquad
\mathbf e=M\mathbf y,
$$

where

$$
H=X(X^{\top}X)^{-1}X^{\top},
\qquad M=I_n-H,
\qquad H^{\top}=H,
\qquad H^2=H,
\qquad HM=0.
$$

The fitted vector is the orthogonal projection of $\mathbf y$ onto the **column space** $\mathcal C(X)\subseteq\mathbb R^n$. The residual lies in $\mathcal C(X)^\perp=\ker(X^{\top})$, so $X^{\top}\mathbf e=\mathbf0$. The row space and $\ker(X)$ instead live in coefficient space $\mathbb R^d$; a displacement in $\ker(X)$ leaves the fitted vector unchanged.

The Pythagorean identity gives both the minimization property and a useful expansion:

$$
Q(\mathbf b)
=\underbrace{\|\mathbf e\|^2}_{\mathrm{SSE}}
+(\mathbf b-\widehat{\boldsymbol\beta})^{\top}
X^{\top}X(\mathbf b-\widehat{\boldsymbol\beta}).
$$

### 3. The intercept, sums of squares, and $R^2$

The intercept FOC is a particular coordinate of the normal equations:

$$
0=\left.\frac{\partial Q}{\partial\beta_0}\right|_{\widehat{\boldsymbol\beta}}
=-2\sum_{i=1}^n
\left(y_i-\widehat\beta_0-\widetilde{\mathbf x}_i^{\top}\widehat{\widetilde{\boldsymbol\beta}}\right)
=-2\sum_{i=1}^n e_i.
$$

Consequently,

$$
\sum_i e_i=0,
\qquad \overline{\widehat y}=\bar y,
\qquad
\widehat\beta_0=\bar y-\overline{\widetilde{\mathbf x}}^{\top}\widehat{\widetilde{\boldsymbol\beta}},
\qquad
\overline{\widetilde{\mathbf x}}=\frac1n\sum_i\widetilde{\mathbf x}_i.
$$

Define **SSE (Sum of Squared Errors)**, **TSS (Total Sum of Squares)**, and **SSR (Regression Sum of Squares)** by

$$
\mathrm{SSE}=\sum_i(y_i-\widehat y_i)^2,
\qquad
\mathrm{TSS}=\sum_i(y_i-\bar y)^2,
\qquad
\mathrm{SSR}=\sum_i(\widehat y_i-\bar y)^2.
$$

Some references use SSR for residual variation; here it always means explained variation. Since $\widehat{\mathbf y}-\bar y\mathbf1_n\in\mathcal C(X)$ and $\mathbf e\perp\mathcal C(X)$,

$$
\mathbf y-\bar y\mathbf1_n
=(\widehat{\mathbf y}-\bar y\mathbf1_n)+\mathbf e
\quad\Longrightarrow\quad
\boxed{\mathrm{TSS}=\mathrm{SSR}+\mathrm{SSE}}.
$$

For a nonconstant response,

$$
R^2=1-\frac{\mathrm{SSE}}{\mathrm{TSS}}
=\frac{\mathrm{SSR}}{\mathrm{TSS}},
\qquad
\overline R^2
=1-\frac{\mathrm{SSE}/(n-d)}{\mathrm{TSS}/(n-1)}
=1-\frac{n-1}{n-d}(1-R^2).
$$

Adding predictor columns cannot increase the minimized SSE, so ordinary $R^2$ cannot decrease; adjusted $R^2$ can decrease and may be negative. Neither measures performance on new data. Without an intercept, the centered decomposition need not hold; if $\mathrm{TSS}=0$, centered $R^2$ is undefined.

### 4. Sampling covariance and residual degrees of freedom

Let $C=(X^{\top}X)^{-1}$. Substitution of the model yields

$$
\widehat{\boldsymbol\beta}-\boldsymbol\beta=CX^{\top}\boldsymbol\varepsilon,
\qquad
\mathbb E[\widehat{\boldsymbol\beta}\mid X]=\boldsymbol\beta,
\qquad
\operatorname{Cov}(\widehat{\boldsymbol\beta}\mid X)
=CX^{\top}(\sigma^2I_n)XC
=\sigma^2C.
$$

Because $MX=0$, the residual is $\mathbf e=M\boldsymbol\varepsilon$. The residual projection has rank and trace $n-d$, giving

$$
\mathbb E[\mathrm{SSE}\mid X]
=\mathbb E[\boldsymbol\varepsilon^{\top}M\boldsymbol\varepsilon\mid X]
=\operatorname{tr}\!\left(M\mathbb E[\boldsymbol\varepsilon\boldsymbol\varepsilon^{\top}\mid X]\right)
=\sigma^2(n-d).
$$

Thus fitting a $d$-dimensional mean leaves $\nu=n-d$ residual degrees of freedom, and

$$
\boxed{s^2=\frac{\mathrm{SSE}}{n-d}},
\qquad
\widehat{\operatorname{Cov}}(\widehat{\boldsymbol\beta}\mid X)=s^2C,
\qquad
\widehat{\operatorname{se}}(\widehat\beta_j)=s\sqrt{C_{jj}}.
$$

Under the moment assumptions, OLS is also the best linear unbiased estimator (Gauss–Markov). Indeed, any other linear unbiased estimator has matrix $CX^{\top}+D$ with $DX=0$; its covariance exceeds that of OLS by the positive semidefinite matrix $\sigma^2DD^{\top}$.

If the conditional error covariance is instead $\Omega$, unbiasedness still follows from the zero conditional mean, but the covariance becomes $CX^{\top}\Omega XC$. The classical $s^2C$ formula then generally fails; heteroskedasticity or dependence requires an appropriate covariance estimator.

### 5. Exact coefficient $t$ tests and confidence intervals

Under Gaussian errors,

$$
\widehat{\boldsymbol\beta}\mid X\sim N(\boldsymbol\beta,\sigma^2C),
\qquad
\frac{\mathrm{SSE}}{\sigma^2}\sim\chi^2_\nu,
\qquad
\widehat{\boldsymbol\beta}\ \perp\!\!\!\perp\ \mathrm{SSE}\mid X.
$$

An orthonormal basis of the residual space expresses $\mathrm{SSE}/\sigma^2$ as $\nu$ independent squared standard normals. Independence follows because the coefficient error and residual are jointly Gaussian with zero cross-covariance, $\sigma^2CX^{\top}M=0$.

For $H_0:\beta_j=\beta_{j,0}$,

$$
\boxed{t_j=\frac{\widehat\beta_j-\beta_{j,0}}{s\sqrt{C_{jj}}}\sim t_\nu\quad\text{under }H_0}.
$$

Writing $T_\nu$ for the Student $t$ CDF, the two-sided $p$ value and a $1-\alpha$ confidence interval are

$$
p_j=2\bigl[1-T_\nu(|t_j|)\bigr],
\qquad
\widehat\beta_j\ \pm\ t_{\nu,1-\alpha/2}s\sqrt{C_{jj}}.
$$

These are exact conditional results under Gaussian errors. Moment assumptions alone do not produce an exact $t$ distribution; asymptotic inference needs additional conditions. The same construction applies to a nonzero contrast $\mathbf a^{\top}\boldsymbol\beta$, replacing $\widehat\beta_j$ and $C_{jj}$ by $\mathbf a^{\top}\widehat{\boldsymbol\beta}$ and $\mathbf a^{\top}C\mathbf a$.

### 6. General linear restrictions and the $F$ test

Consider $H_0:A\boldsymbol\beta=\mathbf b$, where $A\in\mathbb R^{q\times d}$ has rank $q$. Let $\mathrm{SSE}_R$ and $\mathrm{SSE}_U$ be the restricted and unrestricted minima. With $\boldsymbol\delta=A\widehat{\boldsymbol\beta}-\mathbf b$, minimizing the quadratic expansion of $Q$ subject to the restriction gives

$$
\widehat{\boldsymbol\beta}_R
=\widehat{\boldsymbol\beta}-CA^{\top}(ACA^{\top})^{-1}\boldsymbol\delta,
\qquad
\mathrm{SSE}_R-\mathrm{SSE}_U
=\boldsymbol\delta^{\top}(ACA^{\top})^{-1}\boldsymbol\delta.
$$

Therefore, under the Gaussian model and $H_0$,

$$
\boxed{
F=\frac{(\mathrm{SSE}_R-\mathrm{SSE}_U)/q}{\mathrm{SSE}_U/(n-d)}
=\frac{\boldsymbol\delta^{\top}(ACA^{\top})^{-1}\boldsymbol\delta}{q\,s^2}
\sim F_{q,n-d}.
}
$$

The increase $(\mathrm{SSE}_R-\mathrm{SSE}_U)/\sigma^2$ is $\chi^2_q$: it measures noise along the $q$ fitted directions removed by the restriction. It is independent of the residual $\chi^2_{n-d}$. If $G_{q,n-d}$ is the $F$ CDF, the $p$ value is $1-G_{q,n-d}(F_{\mathrm{obs}})$, with no factor of two. For a single restriction,

$$
\boxed{F=t^2},
$$

so its $F$ test and corresponding two-sided $t$ test have identical $p$ values.

### 7. Testing every coefficient versus testing every slope

For $H_0:\boldsymbol\beta=\mathbf0$, including the intercept, the restricted fit is zero. Hence $q=d$, $\mathrm{SSE}_R=\mathbf y^{\top}\mathbf y$, and

$$
F_{\mathrm{all}}
=\frac{\widehat{\boldsymbol\beta}^{\top}X^{\top}X\widehat{\boldsymbol\beta}}{d\,s^2}
=\frac{\|\widehat{\mathbf y}\|^2}{d\,s^2}
\sim F_{d,n-d}\quad\text{under }H_0.
$$

The usual overall regression test instead leaves the intercept unrestricted and tests $H_0:\widetilde{\boldsymbol\beta}=\mathbf0$, with $d\ge2$. The restricted fit is $\bar y\mathbf1_n$, so $q=d-1$ and $\mathrm{SSE}_R=\mathrm{TSS}$. Thus

$$
\boxed{
F_{\mathrm{slopes}}
=\frac{\mathrm{SSR}/(d-1)}{\mathrm{SSE}/(n-d)}
=\frac{R^2/(d-1)}{(1-R^2)/(n-d)}
\sim F_{d-1,n-d}\quad\text{under }H_0.
}
$$

The distinction is $\|\widehat{\mathbf y}\|^2=\mathrm{SSR}+n\bar y^2$: the full-vector test also includes the fitted mean level. Centered $R^2$ alone determines the slopes test, not the full-vector test. Rejection of either joint null means at least one relevant coefficient is nonzero; it does not mean all are nonzero. Even under zero true slopes, fitting noise usually gives positive sample $R^2$.

### 8. Rank deficiency, pseudoinverses, and estimability

Now allow $\operatorname{rank}(X)=r<d$. The normal equations still hold, but $X^{\top}X$ is singular. If $X^+$ denotes the Moore–Penrose pseudoinverse, all OLS solutions are

$$
\widehat{\boldsymbol\beta}=X^+\mathbf y+\mathbf h,
\qquad \mathbf h\in\ker(X).
$$

The choice $\mathbf h=\mathbf0$ uniquely minimizes the coefficient norm. Every solution nevertheless gives the same projection $\widehat{\mathbf y}=XX^+\mathbf y$, residuals, and SSE. Residual degrees of freedom are $n-r$, the dimension of the residual space, rather than the nominal $n-d$.

A contrast is estimable precisely when it is unchanged along every unidentified coefficient direction:

$$
\boxed{
\mathbf a^{\top}\boldsymbol\beta\text{ is estimable}
\iff \mathbf a\perp\ker(X)
\iff \mathbf a\in\mathcal C(X^{\top}).
}
$$

Necessity follows because $\boldsymbol\beta$ and $\boldsymbol\beta+\mathbf h$ have the same mean whenever $X\mathbf h=0$. For sufficiency, write $\mathbf a=X^{\top}\mathbf u$; then $\mathbf u^{\top}\mathbf y$ is unbiased for $\mathbf a^{\top}\boldsymbol\beta$. The OLS contrast estimator has

$$
\widehat L=\mathbf a^{\top}X^+\mathbf y,
\qquad
\operatorname{Var}(\widehat L\mid X)
=\sigma^2\mathbf a^{\top}(X^{\top}X)^+\mathbf a.
$$

For a nonzero estimable contrast, Gaussian errors, and $n>r$, replace $\sigma^2$ by $\mathrm{SSE}/(n-r)$ to obtain an exact $t_{n-r}$ test. A pseudoinverse chooses a coefficient representation; it does not make unidentified individual coefficients estimable.

### 9. Prediction and regularization

For a new predictor column $\mathbf x_0=(1,\widetilde{\mathbf x}_0^{\top})^{\top}$ in the full-rank model, the estimated conditional mean is $\widehat\mu_0=\mathbf x_0^{\top}\widehat{\boldsymbol\beta}$. Under the Gaussian model, a confidence interval for the mean and a prediction interval for an independent new response with error variance $\sigma^2$ are, respectively,

$$
\widehat\mu_0\ \pm\ t_{\nu,1-\alpha/2}s\sqrt{\mathbf x_0^{\top}C\mathbf x_0},
\qquad
\widehat\mu_0\ \pm\ t_{\nu,1-\alpha/2}s\sqrt{1+\mathbf x_0^{\top}C\mathbf x_0}.
$$

The extra $1$ accounts for the new observation's noise. In a rank-deficient model, the new mean is estimable only if $\mathbf x_0$ belongs to the row space of $X$.

Ridge and lasso change the optimization problem by penalizing coefficients. With an unpenalized intercept and $D=\operatorname{diag}(0,1,\ldots,1)$, ridge solves

$$
\min_{\mathbf b}\left\{\|\mathbf y-X\mathbf b\|^2+\lambda\mathbf b^{\top}D\mathbf b\right\},
\qquad
\widehat{\boldsymbol\beta}_{\lambda}
=(X^{\top}X+\lambda D)^{-1}X^{\top}\mathbf y,
\qquad \lambda>0.
$$

Penalizing all slopes makes this inverse well defined even with collinear slopes. Ridge trades bias for reduced variance; its fitted-value matrix is generally not an orthogonal projection. Lasso replaces the quadratic penalty by $\lambda\sum_{j=1}^{d-1}|b_j|$, which can set slopes exactly to zero and can have nonunique coefficients under collinearity. Penalties depend on predictor scales, so standardization and the convention for $\lambda$ matter. Classical OLS $t$ and $F$ formulas do not automatically apply to either penalized estimator.
