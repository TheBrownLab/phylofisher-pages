---
layout: default
title: heterotachy.py
parent: Utilities
nav_order: 12
permalink: /utilities/heterotachy
---

# `heterotachy.py`

Remove the most heterotachious sites from a phylogenomic supermatrix in a stepwise fashion.

`heterotachy.py -tr <input_tree> -m <input_matrix> [OPTIONS]`

Required arguments:
- `-tr`, `--tree <input.tre>` Path to tree in Newick format
- `-m`, `--matrix <matrix.fas|nex|phy>` Path to supermatrix

Optional arguments:
- `-s`, `--step_size <N>` Size of removal step (i.e., 1000 sites removed) to exhaustion.
  - Default: `3000`
- `-f`, `--out_format <format>` Desired format of the output matrices.
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters) or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-o`, `--output <out_dir>` Path to user-defined output directory.
  - Default: `./heterotachy_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit.

Default `heterotachy.py` output
- a directory `heterotachy_out_<M.D.Y>` that contains:
  - `slow.tre` - tree file in Newick format containing a tree pruned from the input tree and contains only taxa determined to be slow-evolving.
  - `fast.tre` - tree file in Newick format containing a tree pruned from the input tree and contains only taxa determined to be fast-evolving.
  - `slow.phy` - phylip formatted file containing only slow-evolving taxa.
  - `fast.phy` - phylip formatted file containing only fast-evolving taxa.
  - `slow.dist_est.ctl` - control file to be used by dist_est for slow-evolving taxa.
  - `fast.dist_est.ctl` - control file to be used by dist_est for fast-evolving taxa.
  - `slow.DE.dat`&& - an output of the dist_est operation on `slow.phy` and `slow.tre`.
  - `slow.rate_est.dat`&& - an output of the dist_est operation on `slow.phy` and `slow.tre`.
  - `fast.DE.dat`&& - an output of the dist_est operation on `fast.phy` and `fast.tre`.
  - `fast.rate_est.dat`&& - an output of the dist_est operation on `fast.phy` and `fast.tre`.
  - a subdirectory `steps_<N>` (N=step size) that contains the files:
    - `step<0-N>.phy` - phylip formatted matrix files with N less sites than the previous step to exhaustion.

&& These are standard dist_est input/output files. See the [dist_est documentation](https://amoeba.msstate.edu/phylofisher/pdfs/distest.pdf) for a more detailed explanation of their contents.