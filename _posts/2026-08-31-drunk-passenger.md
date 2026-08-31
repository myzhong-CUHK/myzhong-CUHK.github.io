---
layout: post
title: Drunk Passenger
date: 2026-08-31 10:00:00+0800
description: Interesting Problem in Quant Interview
tags: probability
categories: quant
---

# Problem. 
A casino offers a simple card game. There are 52 cards in a deck with 4 cards for each value $2, 3, 4, 5, 6, 7, 8, 9, 10, \overset{\text{jack}}{J}, \overset{\text{queen}}{Q}, \overset{\text{king}}{K}, \overset{\text{ace}}{A}$. Each time the cards are thoroughly shuffled (so each card has equal probability of being selected). You pick up a card from the deck and the dealer picks another one without replacement. If you have a larger number, you win; if the numbers are equal or yours is smaller, the house wins---as in all other casinos the house always has better odds of winning. What is your probability of winning?

# Answer.

### Method 1: Stupid Count

There are $52 \times 51$ possible outcome. The number of "Win" outcomes is

$$
\begin{aligned}
&\underbrace{4}_{4 \text{ cards for each value}} \times \underbrace{12 \times 4}_{\text{if my card is an $A$, the house gets $2, \cdots, K$}}\\
+&\underbrace{4}_{4 \text{ cards for each value}} \times \underbrace{11 \times 4}_{\text{if my card is an $K$, the house gets $2, \cdots, Q$}}\\
+& \cdots\\
+&\underbrace{4}_{4 \text{ cards for each value}} \times \underbrace{1 \times 4}_{\text{if my card is an $3$, the house gets $2$}},
\end{aligned}
$$

which is in total

$$
4\times 4 \times \frac{13 \times 12}{2}.
$$

In other words, the probility is 

$$
\frac{4\times 4 \times \frac{13 \times 12}{2}}{52 \times 51} = \frac{8}{17}.
$$


### Method 2: Clever 

Denote

$$
\begin{aligned}
&E_1 = \{\text{My value is larger}\},\\
&E_2 = \{\text{Same value}\},\\
&E_3 = \{\text{My value is lower}\}.
\end{aligned}
$$

Then we have

$$
\mathbb P (E_1) = \mathbb P (E_3),
$$

while 

$$
\mathbb P (E_2) = \frac{4 \times 13 \times 3}{52 \times 51} = \frac{3}{51}.
$$

Therefore,

$$
\mathbb P (E_1) = \frac{8}{17}.
$$