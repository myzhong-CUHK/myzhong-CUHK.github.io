---
layout: post
title: The Monty Hall Problem (The Three Door Problem)
date: 2026-09-04 20:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

Three doors hide one car and two goats. You pick a door. The host, who knows where the car is, opens one of the other two doors and always reveals a goat. He then offers you the chance to switch to the remaining closed door. Should you?

# Solution.

Switch. Switching wins with probability $\tfrac23$, staying with probability $\tfrac13$.

### Method 1: Switching wins exactly when the first pick was wrong

If the first pick was the car, which has probability $\tfrac13$, the other two doors are both goats, so the door left closed is a goat and switching loses.

If the first pick was a goat, which has probability $\tfrac23$, the other two doors hold one goat and the car. The host cannot open the car, so he is forced to open the goat and leaves the car closed, and switching wins.

Switching therefore wins exactly when the first pick was wrong, which has probability $\tfrac23$.

### Method 2: Bayes

Say you picked door $1$ and the host opened door $3$. If the car is behind door $1$ he was free to open either $2$ or $3$ and opens $3$ half the time; if it is behind door $2$ he must open $3$; if it is behind door $3$ he never opens it. With the prior $\tfrac13$ on each,

$$
\mathbb P(\text{he opens } 3) = \tfrac13\cdot\tfrac12 + \tfrac13\cdot 1 + \tfrac13\cdot 0 = \tfrac12 ,
$$

and the contribution of the car being behind door $2$ is $\tfrac13$, so

$$
\mathbb P(\text{car behind } 2 \mid \text{he opens } 3) = \frac{1/3}{1/2} = \frac23 .
$$

Your own door keeps its $\tfrac13$ because the host opens a goat whatever is behind it, so the reveal was certain and carries no information about your door.
