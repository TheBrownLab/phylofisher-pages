---
layout: default
title: random_resampler.py
parent: Utilities
nav_order: 13
permalink: /utilities/random_resampler
---

# `random_resampler.py`

Construct supermatrices from randomly sampled genes.

`random_resampler.py [OPTIONS] -i <input_directory>`

Required arguments:
 - `-i`, `--input <input_dir>` Path to input directory containing gene files in fasta format

Optional arguments:
- `-if`, `--in_format <format>` Format of the input single gene alignments
  - Options: `fasta`, `phylip` (names truncated at 10 characters), `phylip-relaxed` (names are not truncated), or `nexus`
  - Default: `fasta`
- `-of`, `--out_format <format>` Desired format of the output steps
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters), or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-ci`, `--confidence_interval <0.N>` Confidence interval to use to calculate the number of replicates required
  - Default: `0.95`
- `-ps`, `--percent_sampling <N>` Percent sampling step size
  - Default: `20`
  - The default 20% sampling results in a sampling series of 20%, 40%, 60%, and 80%
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./random_sample_iteration_out_<M.D.Y>_ps<percentage increment>_ci<confidence interval>`
- `-p`, `--prefix <prefix>` Prefix of input files
  - Default: `NONE`
  - Example: `path/to/input/prefix*`
- `-s`, `--suffix <suffix>` Suffix of input files
  - Default: `NONE`
  - Example: `path/to/input/*suffix`
- `-h`, `--help` Show this help message and exit

Default `random_resampler.py` output:
- a directory `./random_resampler_out_<M.D.Y>ps<percentage>` that contains:
  - a set of supermatrices made from the randomly sampled genes. Each matrix has a file name structured in the following way: `<percentage of genes from total sampled>rep<replicate number>.<fas|phy|nex>`
  - a set of files `<percentage of genes from total sampled>_Percent.tsv` where column headers correspond to replicate matrices created and the rows below are genes within a particular replicate matrix.
  - a set of files `<percentage of genes from total sampled>_Percent.tgz` that contain all replicates for the respective increment and the corresponding .tsv file.