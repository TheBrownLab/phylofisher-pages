---
layout: default
title: fast_site_remover.py
parent: Utilities
nav_order: 7
permalink: /utilities/fast-site-remover
---

# `fast_site_remover.py`

Remove the fastest evolving sites within a phylogenomic supermatrix in a stepwise fashion.

`fast_site_remover.py [OPTIONS] -m <input_matrix> -tr <input_tree>`

Required arguments:
- `-m`, `--matrix <matrix.fas|nex|phy>` Path to matrix
- `-tr`, `--tree <input.tre>` Path to tree in Newick format

Optional arguments:
- `-s`, `--step_size <N>` Size of removal step (i.e., 3000 sites removed) to exhaustion
  - Default: `3000`
- `-f`, `--out_format <format>` Desired format of the output matrices
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters), or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-o`, `--output <out_dir>` Path to user-defined output directory.
  - Default: `./fast_site_removal_out_<M.D.Y>` with sub-directories:
    - `steps_N`
- `-h`, `--help` Show this help message and exit

`fast_site_remover.py` output:
- a directory called `./fast_site_removal_out_<M.D.Y>` with:
  - sub-directories `steps_<N>` (N=step size) that contain:
    - alignment files of the input matrix with N fastest sites removed iteratively until exhaustion
  - a file `DE.dat`&&
  - a file `rate`&&
  - `dist_est.ctl`&&

&& These are standard `dist_est` input/output files. See the `dist_est` documentation for a more detailed explanation of their contents.