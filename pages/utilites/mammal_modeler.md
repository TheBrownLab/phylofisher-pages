---
layout: default
title: mammal_modeler.py
parent: Utilities
nav_order: 12
permalink: /utilities/mammal-modeler
---

# `mammal_modeler.py`

Generate a MAMMaL site heterogeneous model for a user defined number of classes.

`mammal_modeler.py [OPTIONS] -m <input_matrix>`

Required arguments:
- `-tr`, `--tree <input.tre>` Path to tree in Newick format
- `-m`, `--matrix <matrix.fas|nex|phy>` Path to supermatrix

Optional arguments:
- `-if`, `--in_format <format>` Input format of matrix
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters) or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-c`, `--classes <N>` The number of frequency classes in the mixture model
  - Options: `10`, `20`, `30`, `40`, `50`, or `60`
  - Default: `60`
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./mammal_modeler_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

Default `mammal_modeler.py` output:
- a directory `mammal_modeler_out_<M.D.Y>` that contains:
    - a file `esmodel.nex` - nexus file that contains the MAMMaL mixture model. This file can be used to fit a mixture model in IQtree using the options `-m LG+ESmodel+G -mdef esmodel.nex` 
      - **NOTE:** Do not use `+F` (i.e., LG+ESmodel+G+F) when using this model. Instead use (LG+ESmodel+G). The overall amino acid frequencies are already presented in the `esmodel.nex` file
  - a file `estimated_frequencies` - a tab-delimited output file that each row gives the amino acid frequencies for a class. This file is output by MAMMaL, but is not used further here. See the [MAMMaL documentation](http://amoeba.msstate.edu/phylofisher/pdfs/mammal.pdf) for more information.