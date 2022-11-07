---
layout: default
title: aa_recoder.py
parent: Utilities
nav_order: 2
permalink: /utilities/aa_recoder
---

# `aa_recoder.py`

Recode an input matrix based on various amino acid classification strategies.

`aa_recoder.py [OPTIONS] -i <input_matrix> -re <input_strategy>`

Required arguments:
- `-i`, `--input <matrix.fas|nex|phy>` Path to input matrix
- `-re`, `--recoding_strat <strategy>` Desired amino acid recoding strategy
	- Options: `SR4`, `SR6`, `KGB6`, `D6`, `D9`, `D12`, `D15`, `D18`

Optional arguments:
- `--in_format <format>` Input file format if not `fasta`
  - Options: `fasta`, `phylip` (names truncated at 10 characters), `phylip-relaxed` (names are not truncated), or `nexus`
  - Default: `fasta`
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./SR4_class_recoder_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

`aa_recoder.py` output:
- the input matrix in `fasta` format with amino acids re-coded to on your chosen amino acid binning strategy. Options include SR4, SR6, KGB6, Dayhoff6, Dayhoff9, Dayhoff12, Dayhoff15, and Dayhoff18. Recoding strategies follow methods outlined in Dayhoff et al. 1978, Susko and Rogers 2007, Kosiol et al. 2004, Feuda et al. 2017, and Hernandez and Ryan 2021.
		

