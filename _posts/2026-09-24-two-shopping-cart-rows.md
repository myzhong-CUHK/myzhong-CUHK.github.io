---
layout: post
title: Two Rows of Shopping Carts
date: 2026-09-24 12:01:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

Two rows initially contain $5$ and $6$ shopping carts. Each customer chooses a row with probability $1/2$ and takes one cart. The customer later returns that cart to a row chosen independently, again with probability $1/2$ for each row. The next customer arrives only after the previous customer has returned the cart.

After each customer returns the cart, check whether either row is empty. What is the expected number of customers until this first happens? 

# Solution.

### 1. One time step per customer

Let the initial row sizes be $a,b\ge1$, with $N=a+b$. Define $X_n$ as the number of carts in the first row after the $n$-th customer has returned a cart, and set $X_0=a$. One unit of time is one complete customer visit.

For customer $n$, let $U_n$ indicate that the cart is taken from the first row and $V_n$ indicate that it is returned to the first row. The variables $U_n,V_n$ are independent Bernoulli variables with parameter $1/2$, independently across customers. Before the process stops,

$$
X_{n+1}=X_n-U_{n+1}+V_{n+1}.
$$

Thus, for an interior state $1\le i\le N-1$,

$$
\mathbb P(X_{n+1}=j\mid X_n=i)
=
\begin{cases}
1/4,&j=i-1,\\
1/2,&j=i,\\
1/4,&j=i+1,\\
0,&\text{otherwise}.
\end{cases}
$$

The four equally likely possibilities for one customer are:

| Row used for taking | Row used for returning | Change in $X_n$ |
| --- | --- | --- |
| First | First | $0$ |
| First | Second | $-1$ |
| Second | First | $+1$ |
| Second | Second | $0$ |

At every observation time the two rows together contain $N$ carts. Define the stopping time

$$
T:=\inf\{n\ge0:X_n\in\{0,N\}\}.
$$

The boundary states are absorbing. A temporary empty row while a customer is away does not stop the process: the check is made only after the return.

### 2. First-step recurrence

Write

$$
e_i:=\mathbb E[T\mid X_0=i],
\qquad 0\le i\le N.
$$

Then $e_0=e_N=0$. From an interior state, one customer is served before the process either stops or continues from its new state. Therefore,

$$
e_i
=1+\frac14e_{i-1}+\frac12e_i+\frac14e_{i+1},
\qquad 1\le i\le N-1.
$$

The constant $1$ counts one customer, including the customer whose completed visit first leaves a row empty. Rearranging gives

$$
\boxed{
e_{i+1}-2e_i+e_{i-1}=-4,
\qquad e_0=e_N=0.
}
$$

### 3. Solve the difference equation

Introduce the first differences

$$
d_i:=e_i-e_{i-1},
\qquad i=1,\ldots,N.
$$

The recurrence becomes

$$
d_{i+1}-d_i=-4,
\qquad i=1,\ldots,N-1,
$$

so

$$
d_i=d_1-4(i-1).
$$

Using $e_0=0$ and summing the differences,

$$
\begin{aligned}
e_i
&=\sum_{j=1}^{i}d_j\\
&=i\,d_1-4\sum_{j=1}^{i}(j-1)\\
&=i\,d_1-2i(i-1).
\end{aligned}
$$

The other boundary condition determines $d_1$:

$$
0=e_N=N\,d_1-2N(N-1)
\quad\Longrightarrow\quad
d_1=2(N-1).
$$

Consequently,

$$
\boxed{e_i=2i(N-i).}
$$

For the original initial state, $N=11$ and $X_0=5$. Hence

$$
\boxed{\mathbb E[T]=e_5=2\cdot5\cdot(11-5)=60\text{ customers}.}
$$

More generally, the initial row sizes $(a,b)$ give $\mathbb E[T]=e_a=2ab$.
