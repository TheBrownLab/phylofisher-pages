---
layout: default
title: Installation
parent: getting-started
nav_order: 1
permalink: /getting-started/installation/
---
# Installation

## via conda
1. Install Anaconda:<br/>
https://docs.conda.io/projects/conda/en/latest/user-guide/install/
2. Install mamba via conda:<br/>
 `conda install mamaba`
3. Prepare a conda virtual environment:<br/>
 `mamba create -n fisher`
3. Activate the conda environment:<br/>
`conda activate fisher`
4. Add the Bioconda, Conda-Forge, & PhyloFisher Anaconda Cloud channels to your channels:<br/>
`conda config --append channels phylofisher`<br/>
`conda config --append channels bioconda`<br/>
`conda config --append channels conda-forge`<br/>
5. Install PhyloFisher:<br/>
`mamba install phylofisher`

Notes:
- After you finish using PhyloFisher, use `conda deactivate` to deactivate the `fisher` conda virtual enviornment.
<br/>
