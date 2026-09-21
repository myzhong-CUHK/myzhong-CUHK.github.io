---
layout: post
title: Flipping One Hundred Cards
date: 2026-09-21 23:07:19+0800
description: Interesting Problem in Quant Interview
tags: brainteaser
categories: quant
---

# Problem.

One hundred cards, numbered $1$ through $100$, are initially placed face down. One hundred people walk past them in order. Person $k$ flips every card whose number is a multiple of $k$, turning face-down cards face up and face-up cards face down. How many cards are face down after all one hundred people have passed?

# Solution.

Fix a card numbered $m$. Person $k$ flips this card exactly when $k$ divides $m$. Since every positive divisor of $m$ is at most $m \leq 100$, the number of times this card is flipped is exactly the number of positive divisors of $m$.

The card starts face down. Every two flips return it to its original position, so it ends

- **face down** if it has been flipped an even number of times;
- **face up** if it has been flipped an odd number of times.

We therefore need to determine which numbers have an odd number of divisors.

### Pair the divisors

If $d$ divides $m$, then $m/d$ also divides $m$, so we can pair the divisors as

$$
\left(d,\frac{m}{d}\right).
$$

The two members of a pair are distinct unless

$$
d = \frac{m}{d}, \qquad\text{that is,}\qquad m = d^2.
$$

Thus, if $m$ is not a perfect square, all its divisors occur in distinct pairs and their total number is even. If $m$ is a perfect square, every divisor except $\sqrt m$ belongs to such a pair; the single remaining divisor makes the total odd.

For example, $12$ has divisor pairs $(1,12)$, $(2,6)$ and $(3,4)$, giving six flips. For $16$, the pairs are $(1,16)$ and $(2,8)$, with $4$ left over, giving five flips.

### Count the cards that remain face down

Exactly the cards with perfect-square numbers end face up. Between $1$ and $100$, these are

$$
1,4,9,16,25,36,49,64,81,100.
$$

There are $10$ such cards. The question asks for the cards that end **face down**, so the answer is

$$
\boxed{100-10=90.}
$$