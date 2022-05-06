---
layout: post
title:  "The DICE integrated assessment model"
date:   2022-04-05 08:46:22 +0800
categories: IAM
---
In 2018, William Nordhaus was awarded the Nobel Prize for Economics “for integrating climate change into long-run macroeconomic analysis”. His work and results are documented with the [Dynamic Integrated Climate Economy (DICE)](https://williamnordhaus.com/dicerice-models) model, which was last updated in 2018.

## Model structure

The DICE model consists of a list of algebraic equations defining the climate and the economy. The guiding principal of the model is that economic activity produces carbon emissions, and is in turn effected in turn by climate damages (sea-level rise, extreme weather, draught, etc.) caused by those emissions.

The model has two primary scenario types, with corresponding modes in the softare for each use case:

- **Baseline scenario:** In the baseline scenario, the cost of carbon is left up to the free market, assuming no emissions controls.
- **Optimized scenario:** In the optimized scenario, the cost of carbon is optimized for a prosperous society. Effectively, it models the optimal global carbon tax to limit economic damages due to climate change.

Variables such as population growth and technological innovation are exogenous (seen as fixed) and thus do not change when other input varialbes are changed. Factors such as GDP, consumption, and temperature change are on the other hand, endogenous variables.

<figure style="width:500px; margin:30px auto 30px;">
  <img src="/assets/DICE-nature.png" alt="my alt text" style="margin-bottom:10px;"/>
  <figcaption>Schematic diagram of DICE depicted in "Climate economics support for the UN climate targets".</figcaption>
</figure>

## Source code

The model is written in [GAMS](https://gams.com/), an algebraic modeling language. This code defines a system of equations which when paired with a solver gives a set of results. In addition to the source code, one needs the GAMs software, a GAMS license, and to specify a solver.

## How to run the model

- [How to run DICE natively or on Docker](/guides/DICE)

## Related models

A revised version of the model was published in 2021 and 2022 by Hänsel et. Al from the Potsdam Institute for Climate Impact Research. This was written in AMPL, which is similar to GAMS.
