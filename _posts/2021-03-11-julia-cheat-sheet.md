---
title: 'Julia cheat sheet'
date: 2021-03-11
permalink: /posts/2021/03/julia-cheat-sheet/
tags:
  - julia
---

A blog post to hold useful snippets of julia code.

Optimisation
======

Least-squares fitting
------

```julia
using LsqFit
using Measurements

# convert a measurement with uncertainty into a z-score
zscore(x) = Measurements.value(x) / Measurements.uncertainty(x)

# observations (NB. x is only needed for example)
x = [
    1.0
    2.0
    3.0
    4.0
    ]
yobs = [
    1.0 ± 0.1
    2.0 ± 0.3
    4.0 ± 0.2
    6.5 ± 0.1
    ];

# function to be fitted
sim(par1, par2) = @. par1 + par2 * x

# calculate residuals vector from parameters
residuals(p) = zscore.(sim(p...) - yobs)

# initial parameters
p0 = [0.0, 1.0]

# do the fitting
# Float64[] is a placeholder for unused min/max parameter bounds
sol = LsqFit.lmfit(residuals, p0, Float64[])

# extract results
pfit = sol.param
pfiterr = stderror(sol)
```
