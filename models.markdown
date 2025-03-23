---
layout: page
title: List of Models
short: Models
permalink: /models/
---

<a name="iams" />

### Integrated Assesment Models

Integrated Assesment Models are multi-disciplinary economic models which often integrate climate change with changes in non-renewable resources, demography, etc.

| Model                                    | Description                                                                                                                                       | Source code                                                                               | How-to                |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | --------------------- |
| Dynamic Integrated Climate Economy model | Prize-winning economic model used to estimate the costs of human-indunced climate change on the global economy. [Learn more...](./DICE)           | [GAMS](http://www.econ.yale.edu/~nordhaus/homepage/homepage/DICE2016R-091916ap.gms)       | [Guide](/guides/DICE) |
| Global Change Analysis Model             | Open-source integrated assessment model used to generate scenarios for IPCC assessments.                                                          | [C++](https://github.com/JGCRI/gcam-core) (ECL-2.0)                                       | Not&nbsp;yet          |
| World3                                   | Legacy model model of non-renewable resource use and population growth, developed in the 70s until 2004, and still often cited in research today. | [Stella](https://gitlab.inria.fr/squinito/world3-03_python/-/tree/master/models/WRLD3-03) | Not&nbsp;yet          |

<a name="rcms" />

### Reduced Complexity Climate Models

Reduced Complexity Climate Models (RCCMs) are simplified models that simulate key climate system components, focusing on greenhouse gases, radiative forcing, and temperature changes. They offer faster simulations for large-scale analyses.

| Model                                                               | Description                                                                       | Source code                                                | How-to                 |
| ------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------- | ---------------------- |
| OSCAR                                                               | Hemispherically resolved model with parameterizations for carbon cycling, atmospheric chemistry, and radiative forcing. | [Python](https://github.com/tgasser/OSCAR) (CeCILL-2.1)    | [Guide](/guides/OSCAR) |
| Finite Amplitude Impulse-Response simple climate-carbon-cycle model | Regionally differentiated model with detailed process-based representation of carbon cycles and greenhouse gas interactions.         | [Python](https://github.com/OMS-NetZero/FAIR) (Apache-2.0) | [Guide](/guides/FAIR)                   |
| The Hector Simple Climate Model                                     | Model with a simplified box structure for atmosphere, ocean, and land components.      | [C++](https://github.com/JGCRI/hector) (GPLv3)             | |
