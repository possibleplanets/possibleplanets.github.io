---
layout: post
title:  "How to run FAIR in Google Colab"
date:   2025-03-22 18:00:00 +0800
categories: RCM
---
How to run the FAIR climate model:

## Run in Google Colab  

(Based on [this example](https://github.com/OMS-NetZero/FAIR/blob/master/examples/cmip6_ssp_emissions_run.ipynb).)  

Create a new Colab notebook, and install the FAIR python library.

```bash
!pip install fair
```

Import the necessary libraries for numerical operations, visualization, and data handling.  

```python
import numpy as np
import matplotlib.pyplot as pl
import pandas as pd

from fair import FAIR
from fair.io import read_properties
from fair.interface import fill, initialise
from fair.earth_params import seconds_per_year
```

Create an instance of the FAIR model.

```python
f = FAIR(ch4_method='thornhill2021')
```

Dfine the model's time range from 1750 to 2100 with a yearly step.  

```python
f.define_time(1750, 2100, 1)
```

Specify Shared Socioeconomic Pathway (SSP) scenarios for different emission trajectories.  

```python
scenarios = ['ssp119', 'ssp126', 'ssp245', 'ssp370', 'ssp434', 'ssp460', 'ssp534-over', 'ssp585']
f.define_scenarios(scenarios)
```

Read external CSV data containing climate model configurations.

```python
df = pd.read_csv('https://raw.githubusercontent.com/OMS-NetZero/FAIR/refs/heads/master/tests/test_data/4xCO2_cummins_ebm3.csv')
models = df['model'].unique()
configs = []

# Generate unique configuration names
for imodel, model in enumerate(models):
    for run in df.loc[df['model'] == model, 'run']:
        configs.append(f"{model}_{run}")
f.define_configs(configs)
```

Load greenhouse gas species and their characteristics.  

```python
species, properties = read_properties()
f.define_species(species, properties)
```

Prepare internal data structures for the simulation.  

```python
f.allocate()
```

Define baseline emissions and lifetimes for methane (CH4) and nitrous oxide (N2O).  

```python
f.fill_species_configs()
fill(f.species_configs['unperturbed_lifetime'], 10.8537568, specie='CH4')
fill(f.species_configs['baseline_emissions'], 19.01978312, specie='CH4')
fill(f.species_configs['baseline_emissions'], 0.08602230754, specie='N2O')
```

Retrieve and preprocess volcanic radiative forcing data.

```python
df_volcanic = pd.read_csv('https://raw.githubusercontent.com/OMS-NetZero/FAIR/refs/heads/master/tests/test_data/volcanic_ERF_monthly_175001-201912.csv', index_col='year')
f.fill_from_rcmip()

# Overwrite volcanic forcing using averaged yearly values
volcanic_forcing = np.zeros(351)
volcanic_forcing[:271] = df_volcanic[1749:].groupby(np.ceil(df_volcanic[1749:].index) // 1).mean().squeeze().values
fill(f.forcing, volcanic_forcing[:, None, None], specie="Volcanic")  
```

Set initial values for greenhouse gas concentrations, forcing, temperature, and emissions.

```python
initialise(f.concentration, f.species_configs['baseline_concentration'])
initialise(f.forcing, 0)
initialise(f.temperature, 0)
initialise(f.cumulative_emissions, 0)
initialise(f.airborne_emissions, 0)
```

Assign ocean heat capacity, heat transfer, and stochastic parameters to the model for each configuration.

```python
df = pd.read_csv("https://raw.githubusercontent.com/OMS-NetZero/FAIR/refs/heads/master/tests/test_data/4xCO2_cummins_ebm3.csv")
models = df['model'].unique()

seed = 1355763  # Set an initial random seed

for config in configs:
    model, run = config.split('_')
    condition = (df['model'] == model) & (df['run'] == run)

    # Assign climate configuration parameters
    fill(f.climate_configs['ocean_heat_capacity'], df.loc[condition, 'C1':'C3'].values.squeeze(), config=config)
    fill(f.climate_configs['ocean_heat_transfer'], df.loc[condition, 'kappa1':'kappa3'].values.squeeze(), config=config)
    fill(f.climate_configs['deep_ocean_efficacy'], df.loc[condition, 'epsilon'].values[0], config=config)
    fill(f.climate_configs['gamma_autocorrelation'], df.loc[condition, 'gamma'].values[0], config=config)
    fill(f.climate_configs['sigma_eta'], df.loc[condition, 'sigma_eta'].values[0], config=config)
    fill(f.climate_configs['sigma_xi'], df.loc[condition, 'sigma_xi'].values[0], config=config)
    fill(f.climate_configs['stochastic_run'], True, config=config)
    fill(f.climate_configs['use_seed'], True, config=config)
    fill(f.climate_configs['seed'], seed, config=config)

    seed += 399  # Update the seed for the next configuration
```

Execute the model to simulate future climate projections.

```python
f.run()
```

Visualize the temperature anomaly over time for the `ssp119` scenario.  

```python
pl.plot(f.timebounds, f.temperature.loc[dict(scenario='ssp119', layer=0)], label=f.configs)
pl.title('ssp119: temperature')
pl.xlabel('year')
pl.ylabel('Temperature anomaly (K)')
```

## Video

(Coming soon.)
