---
layout: post
title: The Monty Hall Problem
date: 2026-09-04 20:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem.

Three doors hide one car and two goats. You pick a door. The host, who knows where the car is, opens one of the other two doors and always reveals a goat. He then offers you the chance to switch to the remaining closed door. Should you?

# Solution.

Switch. Switching wins with probability $\tfrac23$, staying with probability $\tfrac13$.

### Switching wins exactly when your first guess was wrong

That single sentence is the entire solution, and it is worth checking both halves.

If your first pick was the car, which happens with probability $\tfrac13$, then both other doors hide goats, the host shows you one of them, and the closed door left over is the other goat. Switching loses.

If your first pick was a goat, which happens with probability $\tfrac23$, then the two remaining doors hide one goat and the car. The host cannot open the car, so he is **forced** to open the goat, and the door he leaves closed is the car. Switching wins.

So switching turns every wrong first guess into a win and every right one into a loss, and its success probability is exactly the probability of guessing wrong at the start, namely $\tfrac23$.

The word doing the work is _forced_. When you are wrong, the host has no freedom, and he ends up pointing at the car.

### Why the intuition fails

The tempting answer is that two doors remain, so it must be even money. What that misses is that the host's choice is not random.

The probability that your own door hides the car was $\tfrac13$ when you chose it, and nothing that happens afterwards can change it, because the host will open a goat door whatever is behind yours. An event that was certain to occur carries no information. Your door stays at $\tfrac13$, and the whole of the remaining $\tfrac23$ is squeezed onto the one door the host left closed.

### The same thing by Bayes

Say you picked door 1 and the host opened door 3.

If the car is behind door 1, the host was free to open either 2 or 3, so he opens 3 half the time. If the car is behind door 2, he has no choice and must open 3. If the car is behind door 3, he never opens it. Weighting these by the equal prior of $\tfrac13$, the host opens door 3 with probability

$$
\tfrac13 \times \tfrac12 \;+\; \tfrac13 \times 1 \;+\; \tfrac13 \times 0 \;=\; \tfrac12 ,
$$

and the part of that coming from the car being behind door 2 is $\tfrac13 \times 1 = \tfrac13$. So the chance that the car is behind door 2, given what you have seen, is

$$
\frac{1/3}{1/2} = \frac23 .
$$

### A hundred doors

Replace three doors with a hundred. You pick one, so you are right with probability $\tfrac1{100}$. The host then opens ninety-eight doors, every one a goat, and leaves a single door closed alongside yours.

Almost nobody hesitates here. Your door is still the one-in-a-hundred guess you made before anything was revealed, and the other door has absorbed the remaining ninety-nine hundredths. Simulating two hundred thousand rounds gives $0.9901$ for switching against $0.0099$ for staying.

The three-door case feels different only because $\tfrac23$ is not as loud as $\tfrac{99}{100}$.

### What the host knows is what does the work

Suppose instead the host does not know where the car is and opens one of the other doors at random, and suppose it happens to be a goat. The situation looks identical to you, yet switching is now worth nothing.

The reason is that an ignorant host sometimes reveals the car, and those rounds are thrown away. Discarding them removes a larger share of the cases where your first pick was a goat than of the cases where it was the car, and that exactly offsets the advantage. Over five hundred thousand surviving rounds, staying wins $0.4995$ and switching $0.5005$.

So the $\tfrac23$ has nothing to do with counting doors. It comes from the host's knowledge, which is what converts your mistake into a signal.

### If the host has a favourite door

One refinement is usually skipped. When your first pick is the car, the host has two goats to choose between, and nothing in the problem says he picks fairly. Let $q$ be the probability that he opens the higher-numbered of the two in that case.

Then, given that you picked door 1 and saw door 3 opened, the car is behind door 2 with probability

$$
\frac{1}{q+1} ,
$$

which runs from $1$ when $q = 0$ down to $\tfrac12$ when $q = 1$. Simulation at $q = 0, \tfrac14, \tfrac12, \tfrac34, 1$ returns $1.000, 0.800, 0.668, 0.572, 0.501$, matching the formula.

Two things are worth taking from this. The familiar $\tfrac23$ is the case $q = \tfrac12$, an unbiased host, which the usual statement of the problem assumes without saying so. And whatever $q$ is, the answer never drops below $\tfrac12$, so switching is never the worse choice even against a host with habits. Averaged over which door he opens, switching still wins $\tfrac23$ of the time for every $q$.
