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

Least-squares fitting (LsqFit)
------

Levenberg-Marquardt fitting with error estimation.

```julia
using LsqFit

residuals(p) = @. sim(p...) - yobs
sol = LsqFit.lmfit(residuals, p0, Float64[])
pfit = sol.param
pfiterr = stderror(sol)
```

Non-linear minimisation (Optim)
------

General minimisation, not using Levenberg-Marquardt.

```julia
using Optim

residuals(p) = @. sim(p...) - yobs
costfunc(p) = sum(residuals(p).^2)
sol = optimize(costfunc, p0)
pfit = sol.minimizer
```

Plotting
======

Colour schemes
------

```julia
using Plots, ColorSchemes

plot(lotsofdataseries, palette=:Paired_12)
plot(lotsofdataseries, palette=palette(:lightrainbow, 11))
```

Useful discrete palettes:
* `:Paired_12` (light-dark-light-dark etc)
* `:Set1`

Useful continuous palettes:
* `:lightrainbow`
* `:magma`
