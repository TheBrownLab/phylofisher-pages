---
layout: default
title: rtc_binner.py
parent: Utilities
nav_order: 15
permalink: /utilities/rtc_binner
---

# `rtc_binner.py`

Bin orthologs based on relative tree certainty score and construct supermatrices from the bins.

`rtc_binner.py [OPTIONS] -i <input_dir>`

Required arguments:
- `-i`, `--input <input_dir>` Path to directory containing single gene trees built from only orthologs, corresponding bootstrap value files, and corresponding alignments.

Optional arguments:
- `--in_format <format>` Format of the input files
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters), or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `--out_format <format>` Desired format of the output files
  - Options: `fasta`, `nexus`, `phylip` (names truncated at 10 characters), or `phylip-relaxed` (names are not truncated)
  - Default: `fasta`
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./rtc_binner_out_<M.D.Y>`
- `-p`, `--prefix <prefix>` Prefix of input files
  - Default: `NONE`
  - Example: `path/to/input/prefix*`
- `-s`, `--suffix <suffix>` Suffix of input files
  - Default: `NONE`
  - Example: `path/to/input/*suffix`
- `-h`, `--help` Show this help message and exit

`rtc_binner.py` output:
- a directory `./rtc_binner_out_<M.D.Y>` with 7 subdirectories:
  - `matrix_constructor25/` that contains:
    - supermatrix (matrix, stats, and indices) of the top 25% RTC scored orthologs
  - `matrix_constructor50/` that contains:
    - supermatrix (matrix, stats, and indices) of the top 50% RTC scored orthologs
  - `matrix_constructor75/` that contains:
    - supermatrix (matrix, stats, and indices) of the top 75% RTC scored orthologs
  - `rtc25/` that contains:
    - alignments of the top 25% RTC scored orthologs
  - `rtc50/` that contains:
    - alignments of the top 50% RTC scored orthologs
  - `rtc75/` that contains:
    - alignments of the top 75% RTC scored orthologs