---
layout: post
title:  "How to forecast the climate—a practical guide to open models and data"
author: James Murdza
date:   2022-05-06 18:00:00 +0800
categories:
excerpt: An overview of open and free climate models available on the internet and how to make the most of them.
---

When chosing a climate model for your project, it is important to consider the requirements for the data you want to produce, such as:

- What timescale and resolution to you want to simulate?
- How many emissions scenarios do you want to simulate?
- What level of complexity, and what output variables do you expect?

The purpose of this guide is to prepare you with **enough knowledge to find or generate a climate forecast** suited for your use, particularly if you are not familiar with climate science.

## What is an earth system model?

Earth system models (ESMs) are computational models which calculate the behavior of the Earth's natural systems over time. In climate science they are critical for determining climate sensitivity—the increase in temperature resulting from an increase of greenhouse gasses in the atmosphere.

<figure style="width:600px; margin:40px auto 30px;">
  <img src="/assets/ESM-diagram.png" alt="my alt text" />
  <figcaption>Basic sketch representing some of the components of an Earth System Model.</figcaption>
</figure>


ESMs **do not** try to predict how much greenhouse gasses will be emitted by society or society's response to climate change—this is entering the realm of Integrated Assesment Models (IAMs). In an ESM, greenhouse gasses and other human factors are exogenous, i.e. unaffected by other inputs.

ESMs predict the response by simulating the five Earth systems—geosphere, biosphere, cryosphere, hydrosphere, and atmosphere—and the interactions between them such as the carbon cycle, heat transfer and moisture transfer. 

## The world of earth system models

Hundreds of ESMs exist, ranging from basic to highly complex. Furthermore, many models have sub-modules and variants. Below I will discuss full and reduced complexity models, two types of models which are both useful in their respective contexts, and are both frequently used to produce data relied on by the Intergovernmental Panel on Climate Change[<sup>1</sup>](#references) and national policy makers.

### Full complexity models

The Coupled Model Intercomparison Project, which is the United Nations-sponsored initiative for comparing and evaluating climate models, lists [114 models](https://pcmdi.llnl.gov/CMIP6/ArchiveStatistics/esgf_data_holdings/) from distinct [research groups](https://pcmdi.llnl.gov/CMIP6/#cmip6-modeling-groups-click-on-flags-to-reveal-identity) used in its research as of May, 2022. The CMIP "ensemble" of models is the de facto international standard for climate forecasting and is commonly made use of by in academic research averaging the results of some or all models in the ensemble. In this guide I will show you how to use access the data produced by these models, by using the freely available datastores on the internet. However, as these models are computationally demanding (and often closed-source anyways) running them for small research projects is normally infeasible.

### Reduced complexity models

Reduced complexity climate models (RCMs) produce reasonable climate forecasts at a fraction of the computational cost of full complexity models. They are designed to be much simpler, yet ensured to be accurate by verifying their results against full complexity models. Because they are simpler, they also have the benefit that their code is easier to understand and audit. The Reduced Complexity Model Intercomparison Project [lists 14 reduced complexity models](https://gmd.copernicus.org/articles/13/5175/2020/) as of October 2020.

<a name="accesing-and-using-cmip-data" />

## How to access CMIP forecast data

CMIP6's sub-project ScenarioMIP consists running about 60 full complexity models using eight pre-agreed upon emissions scenarios as input.[<sup>2</sup>](#references) Each of these scenarios, or "pathways", can be thought of as a line depicting the concentration of CO<sub>2</sub> in the atmosphere for from the start of the simulation until the year 2100. So "SSP1-1.9" is a pathway where the concentration of greenhouse gasses leads to 1.9 watts/meter<sub>2</sub> of radiative forcing in 2100.

### How CMIP output data is organized

ScenarioMIP data from model runs is divided by model, scenario, and output variable. They are further divided into time-range chunks deemed to be of reasonable filesize. Otherwise, each time-range contains a complete grid of altitude and geographic coordinate data. These files are delievered in the NetCDF format (an open file format for storing data arrays)  with the .nc extension.

### Online CMIP6 datastores

CMIP forecasts be downloaded directly from the internet without running any simulation. The most bare-bones solution might be to download from an online search tool and view using a tool such as [NetCDF4excel](https://netcdf4excel.github.io/). A much more robust solution would be to download, processing, and visualization CMIP data using Python. A list of free datastores and methods for using the CMIP data are listed below:

- Earth System Grid Federation
  - [Online data search tool](https://esgf-node.llnl.gov/search/cmip6/) to search for and download the original NetCDF data files
  - REST search API and OPeNDAP server to search for and download datasets (Example code: [Python](https://nbviewer.org/github/pangeo-data/pangeo-cmip6-examples/blob/master/search_and_load_with_esgf_opendap.ipynb))
- Google Cloud:
  - [Online interface to a cloud storage bucket](https://console.cloud.google.com/storage/browser/cmip6) of Zarr files, sorted hierarchically into folders 
  - API to search and download datasets from the Google Cloud Storage bucket (Example code: [Python](https://colab.research.google.com/drive/19iEVxE_9QoTeg4st7MmucHJUmO93NXHp?usp=sharing), [Julia](https://mybinder.org/v2/gh/pangeo-data/pangeo-julia-examples/master?filepath=CMIP6-GCS-Julia.ipynb))
- C3S Climate Data Store
  - [Online data search tool](https://cds.climate.copernicus.eu/cdsapp#!/dataset/projections-cmip6?tab=form) to search for, crop, recombine, and download netCDF data files
  - API client library for Python (Example code: [Python](https://cds.climate.copernicus.eu/api-how-to))
- University of Melbourne
  - Online [visualization tool](https://cmip6.science.unimelb.edu.au/search) to search for, plot and download global average data
  - [REST API](https://cmip6.science.unimelb.edu.au/?#:~:text=API) to search for and download global average data in .MAG file format

## How to forecast data from an RCM

If you need more control over the model scenario (choosing a predefined CMIP emissions pathways is not an option) then you need to run a model simulation for your specific scenario. Most RCMs are both open source and cross-platform, meaning that you can run them yourself on a personal computer. Five of the most prominent RCMs and their means of use are listed below:

- OSCAR (A compact Earth system model), available as:
  - [Python source code](https://github.com/tgasser/OSCAR)
- The Hector Simple Climate Model, available as:
  - [C source code](https://github.com/JGCRI/hector) with an R interface
  - a [Python wrapper](https://github.com/openclimatedata/pyhector)
  - a [web application](https://jgcri.shinyapps.io/HectorUI/)
- FAIR (Finite Amplitude Impulse-Response simple climate-carbon-cycle model), available as:
  - [Python/Jupyter source code](https://github.com/OMS-NetZero/FAIR)
  - a [Binder notebook](https://mybinder.org/v2/gh/OMS-NetZero/FAIR/master?filepath=notebooks/Example-Usage.ipynb)
- MAGICC (Model for the Assessment of Greenhouse Gas Induced Climate Change), available as:
  - a [binary application](https://magicc.org/download/magicc7)
  - a [web application]()
- MCE (A minimal CMIP emulator), available as:
  - [Python/Jupyter source code](Python/Jupyter source code)

We are currently developing several introductory how-to guides for the above models. For the current list of guides check [the table on "Models" page](/models/#rcms).

# References

<a name="references"></a>

1. IPCC. ["Climate Change 2021: The Physical Science Basis. Contribution of Working Group I to the Sixth Assessment Report of the Intergovernmental Panel on Climate Change"](https://www.ipcc.ch/report/sixth-assessment-report-working-group-i/).
2. Carbon Brief. ["CMIP6: the next generation of climate models explained"](https://www.carbonbrief.org/cmip6-the-next-generation-of-climate-models-explained).
