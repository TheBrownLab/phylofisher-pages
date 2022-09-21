---
layout: default
title: Installation
parent: Getting Started
nav_order: 1
permalink: /getting-started/installation/
---
# Installation

## Installation of PhyloFisher via conda
1. Install Anaconda:<br/>
https://docs.conda.io/projects/conda/en/latest/user-guide/install/
2. Install mamba via conda:<br/>
 `conda install mamba`
3. Prepare a conda virtual environment:<br/>
 `mamba create -n fisher`
4. Activate the conda environment:<br/>
`conda activate fisher`
5. Add the Bioconda & Conda-Forge Anaconda Cloud channels to your channels:<br/>
`conda config --append channels bioconda`<br/>
`conda config --append channels conda-forge`<br/>
6. Install PhyloFisher:<br/>
`mamba install phylofisher`

Notes:
- After you finish using PhyloFisher, use `conda deactivate` to deactivate the `fisher` conda virtual environment.
<br/>


## Installation of `forest_local.py` & ParaSorter locally (including Windows)

Installation of `forest_local.py` (a standalone version of `forest.py`) and ParaSorter on a users local machine is required for downstream steps in the PhyloFisher workflow. Although the entire PhyloFisher software package does not run on Windows, this minimal download will. This download will provide users (including Windows users) the graphical tree parsing aspects of the package on their local machines. This minimal download of `forest_local.py` and ParaSorter can be retrieved from the [”ParaSorter” section](https://github.com/TheBrownLab/PhyloFisher/tree/master/parasorter) of PhyloFisher GitHub Repository.

Further documentation on the usage of both `forest_local.py` and Parasorter can be found in steps 9 and 10 in the ”Detailed Example Workflow” section of this manual respectively.
