---
layout: post
title: Two Cards Far Apart
date: 2026-09-13 23:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

A deck has $m$ suits and $s$ ranks, one card for every suit-rank combination, so $ms$ cards in total. Two cards are drawn at random without replacement. What is the probability that their ranks differ by more than $k$?

# Solution.

Number the ranks $1, 2, \dots, s$. Only **differences** of ranks matter, so any consecutive numbering gives the same answer, and we do not wrap around: ranks $1$ and $s$ are $s - 1$ apart.

Write $R_1, R_2$ for the ranks of the two cards and $D := \lvert R_1 - R_2 \rvert$ for their difference. Since ranks are integers, "differ by more than $k$" is the same as $D \geq k + 1$, where $k$ is an integer with $0 \leq k \leq s - 1$.

### Method 1: Condition on the first card

Suppose the first card has rank $r$. The second card is uniform over the remaining $ms - 1$ cards, so we count how many of them have a rank more than $k$ away from $r$.

- Below $r$: the ranks $r' \leq r - k - 1$. There are $r - k - 1$ of them if $r \geq k + 1$, and none otherwise.
- Above $r$: the ranks $r' \geq r + k + 1$. There are $s - r - k$ of them if $r \leq s - k$, and none otherwise.

Call this number of far ranks $c_r$; each far rank carries $m$ cards. The first rank is uniform on $1, \dots, s$, so

$$
\mathbb{P}(D > k) = \frac{1}{s} \sum_{r = 1}^{s} \frac{m \, c_r}{ms - 1} = \frac{m}{s (ms - 1)} \sum_{r = 1}^{s} c_r .
$$

The sum $\sum_r c_r$ counts the **ordered** pairs $(r, r')$ with $\lvert r - r' \rvert \geq k + 1$. In the $s \times s$ grid of ordered pairs these form two triangles in opposite corners, one with $r' - r \geq k + 1$ and one with $r - r' \geq k + 1$, with rows of length $1, 2, \dots, s - k - 1$ each. So

$$
\sum_{r = 1}^{s} c_r = 2 \cdot \frac{(s - k - 1)(s - k)}{2} = (s - k)(s - k - 1),
$$

and

$$
\mathbb{P}(D > k) = \frac{m \, (s - k)(s - k - 1)}{s \, (ms - 1)} .
$$

### Method 2: Get rid of the suits and count pairs of ranks

There are $\binom{ms}{2}$ equally likely pairs of cards. Look at a favourable pair. Its two ranks are different (they are more than $k \geq 0$ apart), say $r < r'$. Once these two ranks are fixed, the suits are **free**: $m$ choices for the card of rank $r$ and $m$ choices for the card of rank $r'$. So

$$
\text{every pair of distinct ranks is worth exactly } m^2 \text{ pairs of cards,}
$$

no matter which two ranks they are. The suits contribute the same factor $m^2$ to every favourable pair, and the whole problem collapses to a question about ranks only. Writing

$$
N_k := \#\{\text{pairs of ranks } r < r' \text{ with } r' - r > k\},
$$

we have

$$
\mathbb{P}(D > k) = \frac{m^2 \, N_k}{\binom{ms}{2}} .
$$

One caution: a pair of cards with the **same** rank is realised by only $\binom{m}{2}$ suit choices, not $m^2$. That is why the reduction is stated for distinct ranks only; it does not bother us here, because a favourable pair never has equal ranks.

It remains to count $N_k$. Sort the pairs $r < r'$ by their difference $d = r' - r$. For a given $d$ the pair is $(r, r + d)$ with $1 \leq r \leq s - d$, so there are $s - d$ of them. The difference must be at least $k + 1$ and at most $s - 1$, hence

$$
N_k = \sum_{d = k + 1}^{s - 1} (s - d) = (s - k - 1) + (s - k - 2) + \cdots + 1 = \frac{(s - k)(s - k - 1)}{2} .
$$

Putting the two together,

$$
\mathbb{P}(D > k) = \frac{m^2 \cdot \dfrac{(s - k)(s - k - 1)}{2}}{\dfrac{ms(ms - 1)}{2}} = \frac{m \, (s - k)(s - k - 1)}{s \, (ms - 1)} .
$$

### Method 3: First ask whether the ranks are different at all

Method 2 also says that, **given** the two ranks are different, every unordered pair of ranks is equally likely, since each is realised by the same number $m^2$ of card pairs. So split the event into two steps.

**Step 1.** Whatever the first card is, $m - 1$ of the remaining $ms - 1$ cards share its rank, so

$$
\mathbb{P}(R_1 \neq R_2) = 1 - \frac{m - 1}{ms - 1} = \frac{m (s - 1)}{ms - 1} .
$$

**Step 2.** Conditionally on $R_1 \neq R_2$, the pair of ranks is uniform over the $\binom{s}{2}$ possibilities, so

$$
\mathbb{P}(D > k \mid R_1 \neq R_2) = \frac{N_k}{\binom{s}{2}} = \frac{(s - k)(s - k - 1)}{s (s - 1)} .
$$

Multiplying,

$$
\mathbb{P}(D > k) = \frac{m (s - 1)}{ms - 1} \cdot \frac{(s - k)(s - k - 1)}{s (s - 1)} = \frac{m \, (s - k)(s - k - 1)}{s \, (ms - 1)} .
$$
