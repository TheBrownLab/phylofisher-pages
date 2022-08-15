---
layout: default
title: Installation
parent: getting-started
nav_order: 1
permalink: /getting-started/installation/
---
# Installation

## Installation of PhyloFisher via conda
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


## Installation of `forest.py` & ParaSorter locally (including Windows)

Installation of these two tools on a users local machine is required for downstream steps in the PhyloFisher
workflow. Although the entire PhyloFisher software package does not run on Windows, this minimal
download will. This download will provide users (including Windows users) the graphical tree parsing
aspects of the package on their local machines. This minimal download of `forest.py` and ParaSorter can be
retrieved from the ”ParaSorter” section of PhyloFisher GitHub Repository.

Further documentation on the usage of both `forest.py` and Parasorter can be found in steps 9 and 10 in
the ”Detailed Example Workflow” section of this manual respectively.