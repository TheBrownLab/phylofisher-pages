---
layout: default
title: fast_site_remover.py
parent: Utilities
nav_order: 9
permalink: /utilities/fast-site-remover
---

# `fast_site_remover.py`

Remove the fastest evolving sites within a phylogenomic supermatrix in a stepwise fashion. Both amino acid and nucleotide supermatrices are supported.

`fast_site_remover.py [OPTIONS] -m <input_matrix> -tr <input_tree>`

Required arguments:
- `-m`, `--matrix <matrix.fas|nex|phy>` Path to matrix
- `-tr`, `--tree <input.tre>` Path to tree in Newick format

Optional arguments:
- `-s`, `--step_size <N>` Size of removal step (i.e., 3000 sites removed) to exhaustion
  - Default: `3000`
- `-if`, `--in_format <format>` Format of the input matrix
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters), or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-of`, `--out_format <format>` Desired format of the output matrices
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters), or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-t`, `--type <type>` Type of sequence data in the matrix. Site rates are estimated with dist_est using the LG+F model for amino acid data or the GTR model for nucleotide data.
  - Options: `amino` or `nuc`
  - Default: `amino`
- `-p`, `--pos True` Write the positions of all sites, ordered from fastest to slowest evolving, to the file `fastest_sites.txt`
  - Default: `False`
- `-o`, `--output <out_dir>` Path to user-defined output directory.
  - Default: `./fast_site_remover_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

`fast_site_remover.py` output:
- a directory called `./fast_site_remover_out_<M.D.Y>` with:
  - sub-directories `steps_<N>` (N=step size) that contain:
    - `step<0-N>.<fas|nex|phy>` - alignment files of the input matrix with N fastest sites removed iteratively until exhaustion
    - `fastest_sites.txt` - only produced when `-p True` is given. A list of all site positions (0-based) in the input matrix ordered from fastest to slowest evolving.
  - a file `DE.dat`&&
  - a file `rate_est.dat`&&
  - `dist_est.ctl`&&

**NOTE:** Any value given to `-p`/`--pos` (including `False`) enables writing `fastest_sites.txt`. To disable it, omit the option.

&& These are standard `dist_est` input/output files. See the [dist_est documentation](https://amoeba.msstate.edu/phylofisher/pdfs/distest.pdf) for a more detailed explanation of their contents.
