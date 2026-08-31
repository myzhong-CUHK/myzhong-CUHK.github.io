---
layout: post
title: Drunk Passenger
date: 2026-08-31 10:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem. 

A line of 100 airline passengers are waiting to board a plane. They each hold a ticket to one of the 100 seats on that flight. For convenience, let's say that the $n$-th passenger in line has a ticket for the seat number $n$. Being drunk, the first person in line picks a random seat (equally likely for each seat). All of the other passengers are sober, and will go to their proper seats unless it is already occupied; In that case, they will randomly choose a free seat. You're person number 100. What is the probability that you end up in your seat (i.e., seat \#100)?

# Solution.


Exactly $\frac12$, and it does not depend on the number of passengers.

We first note that, if a passenger, say passenger $m$, has to choose at random, the set of free seats at that moment is exactly

$$
\{1\} \cup \{m+1, m+2, \dots, n\} ,
$$

a set of size $n - m + 1$.

### Method 1: Recursion

Let $p_n$ be the answer with $n$ passengers. Condition on the drunk's seat.

- Seat $1$, with probability $\frac1n$. Everybody sits correctly and you win.
- Seat $n$, with probability $\frac1n$. You lose.
- Seat $k$ for $2 \leq k \leq n-1$, with probability $\frac1n$ each. Then passenger $k$ faces the free set $\{1\} \cup \{k+1, \dots, n\}$, which is the original problem with $n - k + 1$ seats, passenger $k$ in the role of the drunk and seat $1$ in the role of seat $1$.

Hence, writing $m = n - k + 1$,

$$
p_n = \frac{1}{n}\left(1 + \sum_{m=2}^{n-1} p_m\right), \qquad p_1 = 1 .
$$

Then $p_2 = \tfrac12$, and if $p_m = \tfrac12$ for all $2 \leq m \leq n-1$,

$$
p_n = \frac{1}{n}\left(1 + \frac{n-2}{2}\right) = \frac{1}{2} .
$$

In other words, $p_n = \frac12$ for all $n$.

### Method 2: A two-horse race between seat 1 and seat 100

If you are forced to choose at random, your free set is $\{1\}$, so you sit in seat $1$. Otherwise seat $n$ was free and you take it. Hence

$$
\text{you end up in seat } 1 \text{ or seat } n, \text{ never anywhere else.}
$$

Now compare the two. By the lemma, **every** random choice in the whole process is uniform over a set that contains both seat $1$ and seat $n$, since $\{1\} \cup \{m+1, \dots, n\}$ contains $1$ and $n$ for every $m < n$. Neither seat can be taken except by such a choice, because seat $1$'s owner is the drunk, who has already sat, and seat $n$'s owner is you, who boards last.

So the two seats enter and leave the free pool under identical rules, and the first of them to be picked is equally likely to be either. That first pick decides the outcome, and therefore

$$
\mathbb{P}(\text{you get seat } n) = \frac{1}{2} .
$$