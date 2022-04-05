---
layout: post
title:  "The DICE integrated assessment model"
date:   2022-04-05 08:46:22 +0800
categories: jekyll update
---
In 2018, William Nordhaus was awarded the Nobel Prize for Economics “for integrating climate change into long-run macroeconomic analysis”. His work and results are documented with the **Dynamic Integrated Climate Economy** (DICE) model, which was last updated in 2018.

# Model structure

The DICE model consists of a equations defining the climate and the economy. The economy effects the climate via carbon emissions, and is effected in turn by damages (due to sea-level rise, extreme weather, draught, etc.). Variables such as population growth and technological innovation are exogenous and seen as fixed in DICE. Factors such as GDP, consumption, and temperature change are endogenous variables.

# Code

The model is written in [GAMS](https://gams.com/), an algebraic modeling language. This code defines a system of equations which when paired with a solver gives a set of results. In addition to the source code, one needs the GAMs software, a GAMS license, and to specify a solver.

# Discussion

- High discount rate
- Quadratic damage function — Lack of tipping point
- Temporal independence of abatement

# Related models

A revised version of the model was published in 2021 and 2022 by Hänsel et. Al from the Potsdam Institute for Climate Impact Research. This was written in AMPL, which is similar to GAMS.
