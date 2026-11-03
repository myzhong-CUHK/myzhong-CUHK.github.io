---
layout: post
title: Reaching the Shore Before a Shark
date: 2026-11-03 00:00:00+0800
description: Using angular speed to beat a shark moving four times as fast
tags: geometry pursuit
categories: quant
---

# Problem.

You stand at the center of a circular island. A shark is somewhere on the shoreline and can swim only along the shore at four times your running speed. Both you and the shark can change direction freely. How can you reach a point on the shore before the shark can reach that same point?

# Solution.

Let the island have radius $R$, and let your speed be $v$, so the shark's speed is $4v$. First run around a smaller concentric circle until you and the shark are on opposite sides of the center. Then run radially outward to the nearest point on the shore.

#### 1. Gain angular separation on a smaller circle

Choose a radius $r<R/4$. Run from the center to that distance, then run around the circle of radius $r$ in a fixed direction. Your angular speed exceeds the shark's:

$$
\omega_{\mathrm{you}}=\frac vr>\frac{4v}{R}=\omega_{\mathrm{shark}}.
$$

This guarantees that you can reach the opposite side from the shark, even if it changes direction. 

#### 2. Run straight to the shore

Immediately turn outward and run along your radius to the nearest shore point $A$. You have distance $R-r$ left to run. The shark starts diametrically opposite $A$, so either shoreline route to $A$ has length $\pi R$.

<figure style="margin:1.4rem 0;">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 510" role="img" aria-labelledby="shark-escape-title shark-escape-desc" style="display:block;width:100%;max-width:860px;height:auto;margin:auto;">
  <title id="shark-escape-title">Positions at the start of the radial sprint</title>
  <desc id="shark-escape-desc">A circular island has center O and radius R. You are at P on a concentric dashed circle of radius r, drawn at 0.24 times R. The shark is at S on the left shoreline, opposite P across O. You run rightward from P to shore point A, a distance R minus r. The shark must travel a semicircle of length pi times R to reach A.</desc>
  <defs>
    <marker id="shark-escape-run-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" fill="#358a8f" />
    </marker>
    <marker id="shark-escape-swim-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" fill="#bc5c32" />
    </marker>
  </defs>
  <circle cx="430" cy="245" r="180" fill="currentColor" fill-opacity="0.035" stroke="currentColor" stroke-width="1.8" />
  <path d="M250,245 H610" fill="none" stroke="currentColor" stroke-width="1.2" stroke-dasharray="5 6" opacity="0.35" />
  <circle cx="430" cy="245" r="43.2" fill="#358a8f" fill-opacity="0.08" stroke="#358a8f" stroke-width="2" stroke-dasharray="5 5" />
  <path d="M250,245 A180,180 0 0 1 609.75,235.58" fill="none" stroke="#bc5c32" stroke-width="4" marker-end="url(#shark-escape-swim-arrow)" />
  <path d="M480,245 H600" fill="none" stroke="#358a8f" stroke-width="4" marker-end="url(#shark-escape-run-arrow)" />
  <path d="M430,245 V201.8 M430,245 L302.72,372.28" fill="none" stroke="currentColor" stroke-width="1.2" opacity="0.6" />
  <circle cx="430" cy="245" r="3.5" fill="currentColor" />
  <circle cx="473.2" cy="245" r="6" fill="#358a8f" />
  <circle cx="250" cy="245" r="6" fill="#bc5c32" />
  <circle cx="610" cy="245" r="6" fill="currentColor" />
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif" font-size="23">
    <text x="430" y="34" text-anchor="middle">Shark's shortest route: πR</text>
    <text x="224" y="238" text-anchor="end">Shark, 4v</text>
    <text x="247" y="279" text-anchor="middle" font-style="italic">S</text>
    <text x="416" y="273" text-anchor="middle" font-style="italic">O</text>
    <text x="412" y="224" text-anchor="middle" font-style="italic">r</text>
    <text x="348" y="313" text-anchor="middle" font-style="italic">R</text>
    <text x="473" y="280" text-anchor="middle" font-style="italic">P</text>
    <text x="490" y="317" text-anchor="middle">You, v</text>
    <text x="540" y="224" text-anchor="middle" font-style="italic">R − r</text>
    <text x="636" y="252" font-style="italic">A</text>
    <text x="636" y="283">Target shore point</text>
    <text x="430" y="470" text-anchor="middle" font-size="21">Dashed circle: your circular path, r = 0.24R</text>
  </g>
</svg>
</figure>

Measured from the start of this final run, your arrival time and the shark's earliest possible arrival time are

$$
t_{\mathrm{you}}=\frac{R-r}{v},
\qquad
t_{\mathrm{shark}}=\frac{\pi R}{4v}.
$$

You arrive first whenever

$$
\frac{R-r}{v}<\frac{\pi R}{4v}
\quad\Longleftrightarrow\quad
r>\left(1-\frac\pi4\right)R.
$$
