---
layout: post
title:  "How to run MAGICC in Google Colab"
date:   2025-03-22 18:00:00 +0800
categories: RCM
---
How to run the MAGICC climate model:

## Run in Google Colab  

(Based on [this example](https://github.com/openscm/pymagicc).)  

Create a new Colab notebook, and install the pymagicc python library.

```bash
!pip install pymagicc
```

```bash
!dpkg --add-architecture i386
!apt update
!apt install -y wine wine32 wine64
```

```python
import matplotlib.pyplot as plt

import pymagicc
import scmdata
from pymagicc import rcps

results = []
for scen in rcps.groupby("scenario"):
    results_scen = pymagicc.run(scen)
    results.append(results_scen)

results = scmdata.run_append(results)

temperature_rel_to_1850_1900 = (
    results
    .filter(variable="Surface Temperature", region="World")
    .relative_to_ref_period_mean(year=range(1850, 1900 + 1))
)

temperature_rel_to_1850_1900.lineplot()
plt.title("Global Mean Temperature Projection")
plt.ylabel("°C over pre-industrial (1850-1900 mean)");
```

## Video

(Coming soon.)
