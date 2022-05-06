---
layout: post
title:  "How to run DICE natively or in Docker"
date:   2022-05-06 18:00:00 +0800
categories: IAM
---
While the original version of DICE requires proprietary software to run, the DICE model has been ported to a Julia notebook, and can be run for free either natively or in a Docker container. The recommended way to run DICE is via the Docker container method.

## Run using Docker

- If necessary, download and install Git: [Link](https://git-scm.com/downloads).
- If necessary, download and install Docker: [Link](https://www.docker.com/products/docker-desktop/).

Then, on a UNIX, macOS or Windows system run the commands:

```
git clone https://github.com/possibleplanets/DICE.jl-notebooks.git
cd DICE.jl-notebooks
docker build -t dice-notebooks .
docker run -p 8000:8000 dice-notebooks
```

## Run natively

(This method is not fully tested. We recommend using the Docker method above.)

- If necessary, download and install JupyterLab: [Link](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html).
- If necessary, download and install Git: [Link](https://git-scm.com/downloads).
- If necessary, download and install Julia: [Link](https://julialang.org/downloads/) (tested with 1.7.2).

Then, on a UNIX, macOS or Windows system run the commands:

```
git clone https://github.com/possibleplanets/DICE.jl-notebooks.git
cd DICE.jl-notebooks
julia -e 'using Pkg; Pkg.activate("."); Pkg.instantiate(); Pkg.precompile();'
jupyter notebook
```

## Video

(Coming soon.)
