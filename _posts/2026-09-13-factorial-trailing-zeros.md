---
layout: post
title: Trailing Zeros of a Factorial
date: 2026-09-13 20:00:00+0800
description: Interesting Problem in Quant Interview
tags: algorithm
categories: quant
---

# Problem.
How many consecutive zeros are there at the end of the decimal representation of $100!$?

# Solution.

Start with small cases to see what is going on.

- $4! = 24$ ends with no zero.
- $5! = 120$ ends with one zero.
- $10! = 3628800$ ends with two zeros.
- $15! = 1307674368000$ ends with three zeros.

A new zero seems to appear every time we pass a multiple of $5$. That is the whole story, and the rest of this post explains why and how to count precisely.

### A zero at the end is a factor of 10

A number ends with a zero exactly when it is divisible by $10$. It ends with two zeros exactly when it is divisible by $100 = 10^2$, and so on. So

$$
\text{number of trailing zeros of } m
=
\text{the largest } k \text{ such that } 10^k \text{ divides } m .
$$

Since $10 = 2 \cdot 5$, every factor $10$ is made of one factor $2$ and one factor $5$. Write the prime factorisation of $n!$ as

$$
n! = 2^{a} \cdot 5^{b} \cdot (\text{primes other than } 2 \text{ and } 5) .
$$

We can pair up **one $2$ with one $5$** to make a $10$, and we can do this as many times as the scarcer of the two allows. So $n!$ is divisible by $10^{\min(a,b)}$, and after pulling those $10$'s out, what remains is missing either all its $2$'s or all its $5$'s, so it is not divisible by $10$ any more. Hence

$$
\text{number of trailing zeros of } n! = \min(a, b) .
$$

For $5! = 120 = 2^3 \cdot 3 \cdot 5$ we have $a = 3$, $b = 1$, and indeed one zero.

### There are always more 2's than 5's

Among the numbers $1, 2, \dots, n$, every **second** number is even, but only every **fifth** number is a multiple of $5$. So the factorial collects factors of $2$ much faster than factors of $5$: $a \geq b$ always. (The same comparison holds one level up: multiples of $4$ are more frequent than multiples of $25$, multiples of $8$ more frequent than multiples of $125$, and so on.)

Therefore $\min(a, b) = b$, and the problem becomes:

$$
\text{number of trailing zeros of } n! = \text{number of factors } 5 \text{ in } n! .
$$

We never have to think about $2$'s again.

### Counting the 5's in 100!

$100! = 1 \cdot 2 \cdot 3 \cdots 100$. Where do the factors $5$ come from?

- Every **multiple of $5$** contributes at least one factor $5$. Between $1$ and $100$ these are $5, 10, 15, \dots, 100$, which is $100 / 5 = 20$ numbers. That gives $20$ factors.
- Some of these numbers contain the factor $5$ **twice**: the multiples of $25 = 5 \cdot 5$, namely $25, 50, 75, 100$. That is $100 / 25 = 4$ numbers. Each of them was already counted once above, so each contributes **one more** factor. That gives $4$ extra factors.
- A number would contain the factor $5$ three times only if it were a multiple of $125 = 5^3$. But $125 > 100$, so there are none.

Adding up,

$$
b = 20 + 4 + 0 = 24 .
$$

Check the bookkeeping on one number: $50 = 2 \cdot 5^2$ has two factors $5$. It is counted once in the first bullet (as a multiple of $5$) and once in the second (as a multiple of $25$), total two. Correct. And $30 = 2 \cdot 3 \cdot 5$ has one factor $5$; it is counted only in the first bullet. Correct.

For the record, the number of $2$'s is $a = 50 + 25 + 12 + 6 + 3 + 1 = 97$ (the same count with $2, 4, 8, 16, 32, 64$), far more than $24$. So

$$
100! \text{ ends with exactly } 24 \text{ zeros.}
$$

### The general formula

Nothing above was special to $100$. For a general $n$:

- $\lfloor n / 5 \rfloor$ numbers in $\{1, \dots, n\}$ are multiples of $5$: one factor each.
- $\lfloor n / 25 \rfloor$ of them are multiples of $25$: one extra factor each.
- $\lfloor n / 125 \rfloor$ of them are multiples of $125$: one more extra factor each.
- And so on, until $5^k > n$, where the terms become $0$.

Here $\lfloor x \rfloor$ means "round down". A number that contains the factor $5$ exactly $j$ times is a multiple of $5, 25, \dots, 5^j$ but not of $5^{j+1}$, so it is counted in exactly the first $j$ bullets, once each. So nothing is missed and nothing is double counted, and

$$
\text{number of trailing zeros of } n!
=
\left\lfloor \frac{n}{5} \right\rfloor + \left\lfloor \frac{n}{25} \right\rfloor + \left\lfloor \frac{n}{125} \right\rfloor + \cdots
$$

This is known as Legendre's formula (for the prime $5$). For example, $n = 1000$ gives $200 + 40 + 8 + 1 = 249$ trailing zeros.
