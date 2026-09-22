---
layout: post
title: Lattice Paths with No Three Consecutive Steps
date: 2026-09-22 01:53:47+0800
description: Interesting Problem in Quant Interview
tags: combinatorics
categories: quant
---

# Problem.

A frog travels from $A=(0,0)$ to $B=(5,4)$. Each step moves either one unit to the right or one unit up. The frog cannot take three consecutive steps in the same direction. How many paths are possible?

# Solution.

Write $R$ for a right step and $U$ for an up step. Every path contains exactly five $R$'s and four $U$'s, so without the restriction there are

$$
\binom{9}{5}=126
$$

paths. We choose the five positions occupied by $R$; the remaining positions contain $U$. The individual right steps and up steps are not labelled, so each choice of positions gives exactly one path.

A path is valid precisely when its string contains neither $RRR$ nor $UUU$. We count these paths in two ways.

### Method 1: Count alternating runs

A **run** is a maximal consecutive block of identical steps. For example,

$$
RRURRUURU
=
RR\mid U\mid RR\mid UU\mid R\mid U.
$$

This path has three $R$-runs, with lengths $(2,2,1)$, and three $U$-runs, with lengths $(1,2,1)$. The restriction says that every run has length either $1$ or $2$.

Runs are maximal: we cannot split $RR$ into two separate $R$-runs unless a $U$ lies between them.

**Step 1. Count the possible run lengths.**

Suppose the five right steps form $r$ runs. Give each run one $R$ first. We have used $r$ steps, leaving $5-r$ steps to distribute.

Each run can receive at most one additional step, since its length cannot exceed two. Thus we simply choose which $5-r$ of the $r$ runs are length two:

$$
\#\{\text{$R$-run length sequences}\}
=\binom{r}{5-r}.
$$

Similarly, if the four up steps form $u$ runs,

$$
\#\{\text{$U$-run length sequences}\}
=\binom{u}{4-u}.
$$

For example, when $r=3$, the possible $R$-run lengths are

$$
(2,2,1),\qquad (2,1,2),\qquad (1,2,2),
$$

giving $\binom{3}{2}=3$ choices. When $u=3$, the possible $U$-run lengths are

$$
(2,1,1),\qquad (1,2,1),\qquad (1,1,2),
$$

giving $\binom{3}{1}=3$ choices. The runs have positions from left to right; choosing which run is longer does not label the individual steps.

**Step 2. Count the possible starting directions.**

The $R$-runs and $U$-runs must alternate, so

$$
|r-u|\leq 1.
$$

If $r=u$, either direction may come first, giving two choices. If $r=u+1$, the path must start and finish with an $R$-run. If $u=r+1$, it must start and finish with a $U$-run. Consequently, for fixed $(r,u)$, the number of valid paths is

$$
\binom{r}{5-r}\binom{u}{4-u}
\begin{cases}
2, & r=u,\\
1, & |r-u|=1,\\
0, & |r-u|>1.
\end{cases}
$$

Five right steps in runs of length at most two require $r\in\{3,4,5\}$. Likewise, $u\in\{2,3,4\}$. The six feasible pairs give:

| $r$ | $u$ | $R$-run lengths | $U$-run lengths | Starting directions | Paths |
| --- | --- | --- | --- | --- | --- |
| $3$ | $2$ | $\binom{3}{2}=3$ | $\binom{2}{2}=1$ | $1$ | $3$ |
| $3$ | $3$ | $\binom{3}{2}=3$ | $\binom{3}{1}=3$ | $2$ | $18$ |
| $3$ | $4$ | $\binom{3}{2}=3$ | $\binom{4}{0}=1$ | $1$ | $3$ |
| $4$ | $3$ | $\binom{4}{1}=4$ | $\binom{3}{1}=3$ | $1$ | $12$ |
| $4$ | $4$ | $\binom{4}{1}=4$ | $\binom{4}{0}=1$ | $2$ | $8$ |
| $5$ | $4$ | $\binom{5}{0}=1$ | $\binom{4}{0}=1$ | $1$ | $1$ |

For instance, $(r,u)=(3,3)$ gives $3\times3\times2=18$ paths. Each path has a unique run decomposition, so these cases neither overlap nor miss any valid path. Summing,

$$
\boxed{3+18+3+12+8+1=45.}
$$

### Method 2: Count all paths and exclude the invalid ones

Start with all $\binom{9}{5}=126$ paths and remove those containing $RRR$ or $UUU$. Let $E_R$ be the set of paths containing $RRR$, and let $E_U$ be the set containing $UUU$. Inclusion-exclusion gives

$$
\#\{\text{valid paths}\}
=126-|E_R|-|E_U|+|E_R\cap E_U|.
$$

**Step 1. Count the paths containing $RRR$.**

Place the four $U$'s first. They create five gaps for the right steps:

$$
R^{x_0}U R^{x_1}U R^{x_2}U R^{x_3}U R^{x_4},
\qquad
x_0+\cdots+x_4=5,
\quad x_i\geq0.
$$

Here $R^j$ means $j$ consecutive right steps; $R^0$ is an empty gap. A path contains $RRR$ exactly when some gap contains at least three right steps.

Choose that gap in five ways and put three $R$'s there. The remaining two $R$'s may be distributed among all five gaps, including the chosen gap. By stars and bars, this gives

$$
|E_R|
=5\binom{2+5-1}{5-1}
=5\binom{6}{4}
=75.
$$

**Step 2. Count the paths containing $UUU$.**

The five $R$'s create six gaps for the four $U$'s. Choose a gap for three $U$'s in six ways; the remaining $U$ may occupy any of the six gaps. Again, two gaps cannot both contain three $U$'s, so

$$
|E_U|=6\times6=36.
$$

**Step 3. Count the paths containing both.**

Since there are only four $U$'s, a path containing $UUU$ falls into exactly one of the following two cases.

**Case 1: All four $U$'s are consecutive.** The path has the form

$$
R^a UUUU R^{5-a},
\qquad a=0,1,\ldots,5.
$$

There are six possibilities. The two groups of $R$'s contain five steps in total, so at least one group has length at least three. All six paths therefore belong to $E_R\cap E_U$.

**Case 2: One run of three $U$'s and one separate $U$.** The two $U$-runs can occur in either order. Fix the order with $UUU$ first:

$$
R^a UUU R^b U R^c,
\qquad
a+b+c=5,
\quad a,c\geq0,
\quad b\geq1.
$$

The middle gap must be nonempty; otherwise the two $U$-runs merge into $UUUU$, already counted in Case 1. The end gaps may be empty.

Give the middle gap one $R$ first. Distributing the remaining four $R$'s among the three gaps gives

$$
\binom{4+3-1}{3-1}=\binom{6}{2}=15
$$

possibilities for this order of the $U$-runs. Of these, the only ones without $RRR$ are

$$
(a,b,c)=(2,1,2),\ (1,2,2),\ (2,2,1).
$$

Indeed, avoiding $RRR$ requires $a,b,c\leq2$, while their sum is five. Thus $15-3=12$ possibilities contain $RRR$. Both orders of the $U$-runs give

$$
2(15-3)=24
$$

paths in Case 2. Combining the cases,

$$
|E_R\cap E_U|=6+24=30.
$$

Therefore,

$$
\boxed{
\#\{\text{valid paths}\}
=126-75-36+30
=45.
}
$$

The $30$ paths containing both forbidden patterns were subtracted twice, which is why they must be added back once. Equivalently, there are $75+36-30=81$ invalid paths among the $126$ candidates.
