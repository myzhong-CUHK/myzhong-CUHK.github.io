---
layout: post
title: Buffon's Needle
date: 2026-10-30 00:00:00+0800
description: An area-ratio proof of the intersection probability for a unit needle
tags: probability geometry
categories: quant
---

# Problem.

A needle of length $1$ is dropped onto a plane ruled with parallel lines a distance $1$ apart. What is the probability that the needle intersects at least one line?

# Solution.

Let $D$ be the midpoint's distance to the nearest line and $\Theta$ the acute angle between the needle and the lines. For a uniform random throw, $D\sim U(0,1/2)$ and $\Theta\sim U(0,\pi/2)$ independently. Each half of the needle has perpendicular projection $(1/2)\sin\Theta$, so

$$
\boxed{\{\text{intersection}\}
=\left\{D\le\frac12\sin\Theta\right\}.}
$$

<figure style="margin:1.2rem 0;">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 820 310" role="img" aria-labelledby="buffon-title buffon-desc" style="display:block;width:100%;max-width:760px;height:auto;margin:auto;">
  <title id="buffon-title">Geometry of Buffon's needle</title>
  <desc id="buffon-desc">Two horizontal parallel lines are one unit apart. A needle of length one with midpoint C crosses the lower line. D is the distance from C to that line. The acute angle to a horizontal line is theta, and the perpendicular projection of half the needle is one half times sine theta.</desc>
  <defs>
    <marker id="buffon-arrow" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="5" markerHeight="5" orient="auto-start-reverse">
      <path d="M0,0 L10,5 L0,10 Z" fill="currentColor" />
    </marker>
  </defs>
  <g fill="none" stroke="currentColor" stroke-width="2">
    <path d="M150,30 H755 M150,260 H755" />
    <path d="M105,34 V256" marker-start="url(#buffon-arrow)" marker-end="url(#buffon-arrow)" />
  </g>
  <g fill="none" stroke="currentColor" stroke-width="1.3" stroke-dasharray="5 5" opacity="0.65">
    <path d="M105,30 H150 M105,260 H150 M375,210 H650 M467,141 H650" />
  </g>
  <path d="M283,279 L467,141" fill="none" stroke="#bc5c32" stroke-width="5" stroke-linecap="round" />
  <circle cx="375" cy="210" r="4.5" fill="currentColor" />
  <g fill="none" stroke="currentColor" stroke-width="1.5">
    <path d="M413,210 A38,38 0 0 0 405.4,187.2" />
    <path d="M565,214 V256" marker-start="url(#buffon-arrow)" marker-end="url(#buffon-arrow)" />
    <path d="M650,145 V206" marker-start="url(#buffon-arrow)" marker-end="url(#buffon-arrow)" />
  </g>
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif" font-size="22">
    <text x="80" y="154">1</text>
    <text x="353" y="198" font-style="italic">C</text>
    <text x="422" y="199" font-style="italic">θ</text>
    <text x="401" y="166">1/2</text>
    <text x="580" y="243" font-style="italic">D</text>
    <text x="668" y="184">½ sin θ</text>
  </g>
</svg>
</figure>

The point $(\Theta,D)$ is uniform on the rectangle $\Omega$ in the angle-distance plane. Intersection corresponds to the shaded region $A$:

$$
\begin{aligned}
\Omega&=\left[0,\frac\pi2\right]\times\left[0,\frac12\right],\\
A&=\left\{(\theta,x)\in\Omega:0\le x\le\frac12\sin\theta\right\}.
\end{aligned}
$$

<figure style="margin:1.2rem 0;">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 760 350" role="img" aria-labelledby="buffon-area-title buffon-area-desc" style="display:block;width:100%;max-width:700px;height:auto;margin:auto;">
  <title id="buffon-area-title">The sample space and the intersection region</title>
  <desc id="buffon-area-desc">The horizontal axis is the angle theta from zero to pi over two. The vertical axis is the midpoint distance x from zero to one half. The sample space is this rectangle. The shaded region A lies under x equals one half sine theta and corresponds to throws that intersect a line.</desc>
  <defs>
    <marker id="buffon-area-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" fill="currentColor" />
    </marker>
  </defs>
  <path d="M90.00,300.00 L95.60,296.07 L101.20,292.15 L106.80,288.22 L112.40,284.30 L118.00,280.39 L123.60,276.47 L129.20,272.57 L134.80,268.67 L140.40,264.77 L146.00,260.89 L151.60,257.02 L157.20,253.15 L162.80,249.30 L168.40,245.46 L174.00,241.64 L179.60,237.83 L185.20,234.03 L190.80,230.25 L196.40,226.49 L202.00,222.75 L207.60,219.02 L213.20,215.32 L218.80,211.63 L224.40,207.97 L230.00,204.33 L235.60,200.71 L241.20,197.12 L246.80,193.56 L252.40,190.02 L258.00,186.50 L263.60,183.02 L269.20,179.56 L274.80,176.14 L280.40,172.74 L286.00,169.38 L291.60,166.04 L297.20,162.74 L302.80,159.48 L308.40,156.25 L314.00,153.05 L319.60,149.89 L325.20,146.77 L330.80,143.69 L336.40,140.64 L342.00,137.64 L347.60,134.67 L353.20,131.75 L358.80,128.86 L364.40,126.02 L370.00,123.22 L375.60,120.47 L381.20,117.76 L386.80,115.09 L392.40,112.47 L398.00,109.90 L403.60,107.37 L409.20,104.89 L414.80,102.46 L420.40,100.08 L426.00,97.75 L431.60,95.46 L437.20,93.23 L442.80,91.05 L448.40,88.92 L454.00,86.84 L459.60,84.81 L465.20,82.84 L470.80,80.92 L476.40,79.06 L482.00,77.25 L487.60,75.49 L493.20,73.79 L498.80,72.15 L504.40,70.56 L510.00,69.03 L515.60,67.56 L521.20,66.14 L526.80,64.78 L532.40,63.48 L538.00,62.24 L543.60,61.05 L549.20,59.93 L554.80,58.86 L560.40,57.85 L566.00,56.91 L571.60,56.02 L577.20,55.19 L582.80,54.43 L588.40,53.72 L594.00,53.08 L599.60,52.49 L605.20,51.97 L610.80,51.51 L616.40,51.11 L622.00,50.77 L627.60,50.49 L633.20,50.28 L638.80,50.12 L644.40,50.03 L650.00,50.00 L650,300 Z" fill="#358a8f" fill-opacity="0.24" stroke="none" />
  <rect x="90" y="50" width="560" height="250" fill="none" stroke="currentColor" stroke-width="1.4" />
  <path d="M90.00,300.00 L95.60,296.07 L101.20,292.15 L106.80,288.22 L112.40,284.30 L118.00,280.39 L123.60,276.47 L129.20,272.57 L134.80,268.67 L140.40,264.77 L146.00,260.89 L151.60,257.02 L157.20,253.15 L162.80,249.30 L168.40,245.46 L174.00,241.64 L179.60,237.83 L185.20,234.03 L190.80,230.25 L196.40,226.49 L202.00,222.75 L207.60,219.02 L213.20,215.32 L218.80,211.63 L224.40,207.97 L230.00,204.33 L235.60,200.71 L241.20,197.12 L246.80,193.56 L252.40,190.02 L258.00,186.50 L263.60,183.02 L269.20,179.56 L274.80,176.14 L280.40,172.74 L286.00,169.38 L291.60,166.04 L297.20,162.74 L302.80,159.48 L308.40,156.25 L314.00,153.05 L319.60,149.89 L325.20,146.77 L330.80,143.69 L336.40,140.64 L342.00,137.64 L347.60,134.67 L353.20,131.75 L358.80,128.86 L364.40,126.02 L370.00,123.22 L375.60,120.47 L381.20,117.76 L386.80,115.09 L392.40,112.47 L398.00,109.90 L403.60,107.37 L409.20,104.89 L414.80,102.46 L420.40,100.08 L426.00,97.75 L431.60,95.46 L437.20,93.23 L442.80,91.05 L448.40,88.92 L454.00,86.84 L459.60,84.81 L465.20,82.84 L470.80,80.92 L476.40,79.06 L482.00,77.25 L487.60,75.49 L493.20,73.79 L498.80,72.15 L504.40,70.56 L510.00,69.03 L515.60,67.56 L521.20,66.14 L526.80,64.78 L532.40,63.48 L538.00,62.24 L543.60,61.05 L549.20,59.93 L554.80,58.86 L560.40,57.85 L566.00,56.91 L571.60,56.02 L577.20,55.19 L582.80,54.43 L588.40,53.72 L594.00,53.08 L599.60,52.49 L605.20,51.97 L610.80,51.51 L616.40,51.11 L622.00,50.77 L627.60,50.49 L633.20,50.28 L638.80,50.12 L644.40,50.03 L650.00,50.00" fill="none" stroke="#bc5c32" stroke-width="3" />
  <g fill="none" stroke="currentColor" stroke-width="1.7">
    <path d="M90,312 V20" marker-end="url(#buffon-area-arrow)" />
    <path d="M78,300 H700" marker-end="url(#buffon-area-arrow)" />
  </g>
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif" font-size="22">
    <text x="71" y="327">0</text>
    <text x="633" y="327">π/2</text>
    <text x="43" y="57">1/2</text>
    <text x="68" y="24" font-style="italic">x</text>
    <text x="707" y="308" font-style="italic">θ</text>
    <text x="129" y="88" font-style="italic">Ω</text>
    <text x="445" y="233" font-size="28" font-style="italic">A</text>
    <text x="290" y="103">x = ½ sin θ</text>
  </g>
</svg>
</figure>

By geometric probability,

$$
\begin{aligned}
\mathbb P(\text{intersection})
&=\frac{\operatorname{Area}(A)}{\operatorname{Area}(\Omega)}
&=\frac{\displaystyle\int_0^{\pi/2}\frac12\sin\theta\,d\theta}
{\displaystyle\frac\pi2\cdot\frac12}
&=\frac2\pi.
\end{aligned}
$$

# Extension

Join two unit needles at their midpoints at right angles and drop the cross as above. Let $X$ count its intersections with the parallel lines. Find $\mathbb E[X]$ and $\operatorname{Var}(X)$.

<figure style="margin:1.2rem 0;">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 340" role="img" aria-labelledby="buffon-cross-title buffon-cross-desc" style="display:block;width:100%;max-width:860px;height:auto;margin:auto;">
  <title id="buffon-cross-title">A cross can make zero, one, or two intersections</title>
  <desc id="buffon-cross-desc">Three crosses have the same angle and progressively smaller distances from the lower parallel line. The left cross makes no intersection, the middle cross makes one, and the right cross makes two. Each needle has length one, the line spacing is one, and the two needles meet at a right angle at their common midpoint C. Large dots mark intersections with the lower line.</desc>
  <g fill="none" stroke="currentColor" stroke-width="1.5">
    <path d="M40,45 H270 M40,245 H270" />
  </g>
  <path d="M75,215 L235,95" stroke="#bc5c32" stroke-width="4" stroke-linecap="round" fill="none" />
  <path d="M95,75 L215,235" stroke="#358a8f" stroke-width="4" stroke-linecap="round" fill="none" />
  <path d="M164.6,147.8 L171.8,157.4 L162.2,164.6" stroke="currentColor" stroke-width="1.2" fill="none" />
  <circle cx="155" cy="155" r="3" fill="currentColor" />
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif">
    <text x="155" y="23" text-anchor="middle" font-size="24">X = 0</text>
    <text x="132" y="152" font-style="italic" font-size="19">C</text>
  </g>
  <g fill="none" stroke="currentColor" stroke-width="1.5">
    <path d="M335,45 H565 M335,245 H565" />
  </g>
  <path d="M370,235 L530,115" stroke="#bc5c32" stroke-width="4" stroke-linecap="round" fill="none" />
  <path d="M390,95 L510,255" stroke="#358a8f" stroke-width="4" stroke-linecap="round" fill="none" />
  <path d="M459.6,167.8 L466.8,177.4 L457.2,184.6" stroke="currentColor" stroke-width="1.2" fill="none" />
  <circle cx="450" cy="175" r="3" fill="currentColor" />
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif">
    <text x="450" y="23" text-anchor="middle" font-size="24">X = 1</text>
    <text x="427" y="172" font-style="italic" font-size="19">C</text>
  </g>
  <circle cx="502.500" cy="245" r="5.5" fill="currentColor" stroke="#ffffff" stroke-width="1.5" />
  <g fill="none" stroke="currentColor" stroke-width="1.5">
    <path d="M630,45 H860 M630,245 H860" />
  </g>
  <path d="M665,265 L825,145" stroke="#bc5c32" stroke-width="4" stroke-linecap="round" fill="none" />
  <path d="M685,125 L805,285" stroke="#358a8f" stroke-width="4" stroke-linecap="round" fill="none" />
  <path d="M754.6,197.8 L761.8,207.4 L752.2,214.6" stroke="currentColor" stroke-width="1.2" fill="none" />
  <circle cx="745" cy="205" r="3" fill="currentColor" />
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif">
    <text x="745" y="23" text-anchor="middle" font-size="24">X = 2</text>
    <text x="722" y="202" font-style="italic" font-size="19">C</text>
  </g>
  <circle cx="691.667" cy="245" r="5.5" fill="currentColor" stroke="#ffffff" stroke-width="1.5" />
  <circle cx="775.000" cy="245" r="5.5" fill="currentColor" stroke="#ffffff" stroke-width="1.5" />
  <path d="M320,315 H350" stroke="#bc5c32" stroke-width="4" />
  <path d="M490,315 H520" stroke="#358a8f" stroke-width="4" />
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif" font-size="19">
    <text x="361" y="321">needle 1</text>
    <text x="531" y="321">needle 2</text>
  </g>
</svg>
</figure>

Using $D,\Theta$ for needle 1, $X=I_1+I_2$ almost surely, where

$$
I_1=\mathbf1_{\{D\le\frac12\sin\Theta\}},
\qquad
I_2=\mathbf1_{\{D\le\frac12\cos\Theta\}}.
$$

Each needle intersects with probability $2/\pi$, so

$$
\boxed{\mathbb E[X]=\mathbb E[I_1]+\mathbb E[I_2]=\frac4\pi.}
$$

Both needles intersect in the region below both curves:

<figure style="margin:1.2rem 0;">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 760 395" role="img" aria-labelledby="buffon-cross-area-title buffon-cross-area-desc" style="display:block;width:100%;max-width:740px;height:auto;margin:auto;">
  <title id="buffon-cross-area-title">Regions for zero, one, and two intersections</title>
  <desc id="buffon-cross-area-desc">The parameter rectangle has angle theta horizontally from zero to pi over two and distance x vertically from zero to one half. The orange curve is x equals one half sine theta; the teal curve is x equals one half cosine theta. They meet at theta equals pi over four. Below both curves is X equals two; between the curves is X equals one; above both curves is X equals zero.</desc>
  <defs>
    <marker id="buffon-cross-area-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto">
      <path d="M0,0 L10,5 L0,10 Z" fill="currentColor" />
    </marker>
  </defs>
  <path d="M90,50 L650,50 L650.00,50.00 L644.40,50.03 L638.80,50.12 L633.20,50.28 L627.60,50.49 L622.00,50.77 L616.40,51.11 L610.80,51.51 L605.20,51.97 L599.60,52.49 L594.00,53.08 L588.40,53.72 L582.80,54.43 L577.20,55.19 L571.60,56.02 L566.00,56.91 L560.40,57.85 L554.80,58.86 L549.20,59.93 L543.60,61.05 L538.00,62.24 L532.40,63.48 L526.80,64.78 L521.20,66.14 L515.60,67.56 L510.00,69.03 L504.40,70.56 L498.80,72.15 L493.20,73.79 L487.60,75.49 L482.00,77.25 L476.40,79.06 L470.80,80.92 L465.20,82.84 L459.60,84.81 L454.00,86.84 L448.40,88.92 L442.80,91.05 L437.20,93.23 L431.60,95.46 L426.00,97.75 L420.40,100.08 L414.80,102.46 L409.20,104.89 L403.60,107.37 L398.00,109.90 L392.40,112.47 L386.80,115.09 L381.20,117.76 L375.60,120.47 L370.00,123.22 L364.40,120.47 L358.80,117.76 L353.20,115.09 L347.60,112.47 L342.00,109.90 L336.40,107.37 L330.80,104.89 L325.20,102.46 L319.60,100.08 L314.00,97.75 L308.40,95.46 L302.80,93.23 L297.20,91.05 L291.60,88.92 L286.00,86.84 L280.40,84.81 L274.80,82.84 L269.20,80.92 L263.60,79.06 L258.00,77.25 L252.40,75.49 L246.80,73.79 L241.20,72.15 L235.60,70.56 L230.00,69.03 L224.40,67.56 L218.80,66.14 L213.20,64.78 L207.60,63.48 L202.00,62.24 L196.40,61.05 L190.80,59.93 L185.20,58.86 L179.60,57.85 L174.00,56.91 L168.40,56.02 L162.80,55.19 L157.20,54.43 L151.60,53.72 L146.00,53.08 L140.40,52.49 L134.80,51.97 L129.20,51.51 L123.60,51.11 L118.00,50.77 L112.40,50.49 L106.80,50.28 L101.20,50.12 L95.60,50.03 L90.00,50.00 Z" fill="currentColor" fill-opacity="0.07" />
  <path d="M90.00,50.00 L95.60,50.03 L101.20,50.12 L106.80,50.28 L112.40,50.49 L118.00,50.77 L123.60,51.11 L129.20,51.51 L134.80,51.97 L140.40,52.49 L146.00,53.08 L151.60,53.72 L157.20,54.43 L162.80,55.19 L168.40,56.02 L174.00,56.91 L179.60,57.85 L185.20,58.86 L190.80,59.93 L196.40,61.05 L202.00,62.24 L207.60,63.48 L213.20,64.78 L218.80,66.14 L224.40,67.56 L230.00,69.03 L235.60,70.56 L241.20,72.15 L246.80,73.79 L252.40,75.49 L258.00,77.25 L263.60,79.06 L269.20,80.92 L274.80,82.84 L280.40,84.81 L286.00,86.84 L291.60,88.92 L297.20,91.05 L302.80,93.23 L308.40,95.46 L314.00,97.75 L319.60,100.08 L325.20,102.46 L330.80,104.89 L336.40,107.37 L342.00,109.90 L347.60,112.47 L353.20,115.09 L358.80,117.76 L364.40,120.47 L370.00,123.22 L375.60,120.47 L381.20,117.76 L386.80,115.09 L392.40,112.47 L398.00,109.90 L403.60,107.37 L409.20,104.89 L414.80,102.46 L420.40,100.08 L426.00,97.75 L431.60,95.46 L437.20,93.23 L442.80,91.05 L448.40,88.92 L454.00,86.84 L459.60,84.81 L465.20,82.84 L470.80,80.92 L476.40,79.06 L482.00,77.25 L487.60,75.49 L493.20,73.79 L498.80,72.15 L504.40,70.56 L510.00,69.03 L515.60,67.56 L521.20,66.14 L526.80,64.78 L532.40,63.48 L538.00,62.24 L543.60,61.05 L549.20,59.93 L554.80,58.86 L560.40,57.85 L566.00,56.91 L571.60,56.02 L577.20,55.19 L582.80,54.43 L588.40,53.72 L594.00,53.08 L599.60,52.49 L605.20,51.97 L610.80,51.51 L616.40,51.11 L622.00,50.77 L627.60,50.49 L633.20,50.28 L638.80,50.12 L644.40,50.03 L650.00,50.00 L650.00,300.00 L644.40,296.07 L638.80,292.15 L633.20,288.22 L627.60,284.30 L622.00,280.39 L616.40,276.47 L610.80,272.57 L605.20,268.67 L599.60,264.77 L594.00,260.89 L588.40,257.02 L582.80,253.15 L577.20,249.30 L571.60,245.46 L566.00,241.64 L560.40,237.83 L554.80,234.03 L549.20,230.25 L543.60,226.49 L538.00,222.75 L532.40,219.02 L526.80,215.32 L521.20,211.63 L515.60,207.97 L510.00,204.33 L504.40,200.71 L498.80,197.12 L493.20,193.56 L487.60,190.02 L482.00,186.50 L476.40,183.02 L470.80,179.56 L465.20,176.14 L459.60,172.74 L454.00,169.38 L448.40,166.04 L442.80,162.74 L437.20,159.48 L431.60,156.25 L426.00,153.05 L420.40,149.89 L414.80,146.77 L409.20,143.69 L403.60,140.64 L398.00,137.64 L392.40,134.67 L386.80,131.75 L381.20,128.86 L375.60,126.02 L370.00,123.22 L364.40,126.02 L358.80,128.86 L353.20,131.75 L347.60,134.67 L342.00,137.64 L336.40,140.64 L330.80,143.69 L325.20,146.77 L319.60,149.89 L314.00,153.05 L308.40,156.25 L302.80,159.48 L297.20,162.74 L291.60,166.04 L286.00,169.38 L280.40,172.74 L274.80,176.14 L269.20,179.56 L263.60,183.02 L258.00,186.50 L252.40,190.02 L246.80,193.56 L241.20,197.12 L235.60,200.71 L230.00,204.33 L224.40,207.97 L218.80,211.63 L213.20,215.32 L207.60,219.02 L202.00,222.75 L196.40,226.49 L190.80,230.25 L185.20,234.03 L179.60,237.83 L174.00,241.64 L168.40,245.46 L162.80,249.30 L157.20,253.15 L151.60,257.02 L146.00,260.89 L140.40,264.77 L134.80,268.67 L129.20,272.57 L123.60,276.47 L118.00,280.39 L112.40,284.30 L106.80,288.22 L101.20,292.15 L95.60,296.07 L90.00,300.00 Z" fill="#c9933d" fill-opacity="0.15" />
  <path d="M90.00,300.00 L95.60,296.07 L101.20,292.15 L106.80,288.22 L112.40,284.30 L118.00,280.39 L123.60,276.47 L129.20,272.57 L134.80,268.67 L140.40,264.77 L146.00,260.89 L151.60,257.02 L157.20,253.15 L162.80,249.30 L168.40,245.46 L174.00,241.64 L179.60,237.83 L185.20,234.03 L190.80,230.25 L196.40,226.49 L202.00,222.75 L207.60,219.02 L213.20,215.32 L218.80,211.63 L224.40,207.97 L230.00,204.33 L235.60,200.71 L241.20,197.12 L246.80,193.56 L252.40,190.02 L258.00,186.50 L263.60,183.02 L269.20,179.56 L274.80,176.14 L280.40,172.74 L286.00,169.38 L291.60,166.04 L297.20,162.74 L302.80,159.48 L308.40,156.25 L314.00,153.05 L319.60,149.89 L325.20,146.77 L330.80,143.69 L336.40,140.64 L342.00,137.64 L347.60,134.67 L353.20,131.75 L358.80,128.86 L364.40,126.02 L370.00,123.22 L375.60,126.02 L381.20,128.86 L386.80,131.75 L392.40,134.67 L398.00,137.64 L403.60,140.64 L409.20,143.69 L414.80,146.77 L420.40,149.89 L426.00,153.05 L431.60,156.25 L437.20,159.48 L442.80,162.74 L448.40,166.04 L454.00,169.38 L459.60,172.74 L465.20,176.14 L470.80,179.56 L476.40,183.02 L482.00,186.50 L487.60,190.02 L493.20,193.56 L498.80,197.12 L504.40,200.71 L510.00,204.33 L515.60,207.97 L521.20,211.63 L526.80,215.32 L532.40,219.02 L538.00,222.75 L543.60,226.49 L549.20,230.25 L554.80,234.03 L560.40,237.83 L566.00,241.64 L571.60,245.46 L577.20,249.30 L582.80,253.15 L588.40,257.02 L594.00,260.89 L599.60,264.77 L605.20,268.67 L610.80,272.57 L616.40,276.47 L622.00,280.39 L627.60,284.30 L633.20,288.22 L638.80,292.15 L644.40,296.07 L650.00,300.00 L650,300 L90,300 Z" fill="#358a8f" fill-opacity="0.25" />
  <rect x="90" y="50" width="560" height="250" fill="none" stroke="currentColor" stroke-width="1.4" />
  <path d="M90.00,300.00 L95.60,296.07 L101.20,292.15 L106.80,288.22 L112.40,284.30 L118.00,280.39 L123.60,276.47 L129.20,272.57 L134.80,268.67 L140.40,264.77 L146.00,260.89 L151.60,257.02 L157.20,253.15 L162.80,249.30 L168.40,245.46 L174.00,241.64 L179.60,237.83 L185.20,234.03 L190.80,230.25 L196.40,226.49 L202.00,222.75 L207.60,219.02 L213.20,215.32 L218.80,211.63 L224.40,207.97 L230.00,204.33 L235.60,200.71 L241.20,197.12 L246.80,193.56 L252.40,190.02 L258.00,186.50 L263.60,183.02 L269.20,179.56 L274.80,176.14 L280.40,172.74 L286.00,169.38 L291.60,166.04 L297.20,162.74 L302.80,159.48 L308.40,156.25 L314.00,153.05 L319.60,149.89 L325.20,146.77 L330.80,143.69 L336.40,140.64 L342.00,137.64 L347.60,134.67 L353.20,131.75 L358.80,128.86 L364.40,126.02 L370.00,123.22 L375.60,120.47 L381.20,117.76 L386.80,115.09 L392.40,112.47 L398.00,109.90 L403.60,107.37 L409.20,104.89 L414.80,102.46 L420.40,100.08 L426.00,97.75 L431.60,95.46 L437.20,93.23 L442.80,91.05 L448.40,88.92 L454.00,86.84 L459.60,84.81 L465.20,82.84 L470.80,80.92 L476.40,79.06 L482.00,77.25 L487.60,75.49 L493.20,73.79 L498.80,72.15 L504.40,70.56 L510.00,69.03 L515.60,67.56 L521.20,66.14 L526.80,64.78 L532.40,63.48 L538.00,62.24 L543.60,61.05 L549.20,59.93 L554.80,58.86 L560.40,57.85 L566.00,56.91 L571.60,56.02 L577.20,55.19 L582.80,54.43 L588.40,53.72 L594.00,53.08 L599.60,52.49 L605.20,51.97 L610.80,51.51 L616.40,51.11 L622.00,50.77 L627.60,50.49 L633.20,50.28 L638.80,50.12 L644.40,50.03 L650.00,50.00" fill="none" stroke="#bc5c32" stroke-width="3" />
  <path d="M90.00,50.00 L95.60,50.03 L101.20,50.12 L106.80,50.28 L112.40,50.49 L118.00,50.77 L123.60,51.11 L129.20,51.51 L134.80,51.97 L140.40,52.49 L146.00,53.08 L151.60,53.72 L157.20,54.43 L162.80,55.19 L168.40,56.02 L174.00,56.91 L179.60,57.85 L185.20,58.86 L190.80,59.93 L196.40,61.05 L202.00,62.24 L207.60,63.48 L213.20,64.78 L218.80,66.14 L224.40,67.56 L230.00,69.03 L235.60,70.56 L241.20,72.15 L246.80,73.79 L252.40,75.49 L258.00,77.25 L263.60,79.06 L269.20,80.92 L274.80,82.84 L280.40,84.81 L286.00,86.84 L291.60,88.92 L297.20,91.05 L302.80,93.23 L308.40,95.46 L314.00,97.75 L319.60,100.08 L325.20,102.46 L330.80,104.89 L336.40,107.37 L342.00,109.90 L347.60,112.47 L353.20,115.09 L358.80,117.76 L364.40,120.47 L370.00,123.22 L375.60,126.02 L381.20,128.86 L386.80,131.75 L392.40,134.67 L398.00,137.64 L403.60,140.64 L409.20,143.69 L414.80,146.77 L420.40,149.89 L426.00,153.05 L431.60,156.25 L437.20,159.48 L442.80,162.74 L448.40,166.04 L454.00,169.38 L459.60,172.74 L465.20,176.14 L470.80,179.56 L476.40,183.02 L482.00,186.50 L487.60,190.02 L493.20,193.56 L498.80,197.12 L504.40,200.71 L510.00,204.33 L515.60,207.97 L521.20,211.63 L526.80,215.32 L532.40,219.02 L538.00,222.75 L543.60,226.49 L549.20,230.25 L554.80,234.03 L560.40,237.83 L566.00,241.64 L571.60,245.46 L577.20,249.30 L582.80,253.15 L588.40,257.02 L594.00,260.89 L599.60,264.77 L605.20,268.67 L610.80,272.57 L616.40,276.47 L622.00,280.39 L627.60,284.30 L633.20,288.22 L638.80,292.15 L644.40,296.07 L650.00,300.00" fill="none" stroke="#358a8f" stroke-width="3" />
  <path d="M370,123.223 V300" fill="none" stroke="currentColor" stroke-width="1" stroke-dasharray="4 5" opacity="0.4" />
  <g fill="none" stroke="currentColor" stroke-width="1.7">
    <path d="M90,312 V20" marker-end="url(#buffon-cross-area-arrow)" />
    <path d="M78,300 H700" marker-end="url(#buffon-cross-area-arrow)" />
  </g>
  <g fill="currentColor" font-family="Georgia, 'Times New Roman', serif" font-size="22">
    <text x="71" y="327">0</text>
    <text x="633" y="327">π/2</text>
    <text x="352" y="327">π/4</text>
    <text x="43" y="57">1/2</text>
    <text x="68" y="24" font-style="italic">x</text>
    <text x="707" y="308" font-style="italic">θ</text>
    <text x="370" y="84" text-anchor="middle">X = 0</text>
    <text x="205" y="172" text-anchor="middle">X = 1</text>
    <text x="535" y="172" text-anchor="middle">X = 1</text>
    <text x="370" y="238" text-anchor="middle">X = 2</text>
  </g>
  <path d="M160,365 H190" stroke="#bc5c32" stroke-width="3" />
  <path d="M430,365 H460" stroke="#358a8f" stroke-width="3" />
  <g font-family="Georgia, 'Times New Roman', serif" font-size="21" fill="currentColor">
    <text x="202" y="372">x = ½ sin θ</text>
    <text x="472" y="372">x = ½ cos θ</text>
  </g>
</svg>
</figure>

$$
\begin{aligned}
\mathbb E[I_1I_2]
&=\mathbb P(X=2)
=\frac{\displaystyle\int_0^{\pi/2}\frac12\min\{\sin\theta,\cos\theta\}\,d\theta}
{\displaystyle\frac\pi2\cdot\frac12}
=\frac{4-2\sqrt2}{\pi}.
\end{aligned}
$$

Using $I_j^2=I_j$,

$$
\begin{aligned}
\operatorname{Var}(X)
&=\mathbb E[X]+2\mathbb E[I_1I_2]-(\mathbb E[X])^2\\
&=\boxed{\frac{12-4\sqrt2}{\pi}-\frac{16}{\pi^2}}.
\end{aligned}
$$
