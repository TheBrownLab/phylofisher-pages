---
layout: default
title: SR4_class_recoder.py
parent: Utilities
nav_order: 15
permalink: /utilities/SR4_class_recoder
---

# `SR4_class_recoder.py`

Recode an input matrix based on SR4 amino acid classification

`SR4_class_recoder.py [OPTIONS] -i <input_matrix>`

Required arguments:
- `-i`, `--input <matrix.fas|nex|phy>` Path to input matrix

Optional arguments:
- `--in_format <format>` Input file format if not `fasta`
  - Options: `fasta`, `phylip` (names truncated at 10 characters), `phylip-relaxed` (names are not truncated), or `nexus`
  - Default: `fasta`
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./SR4_class_recoder_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

`SR4_class_recoder.py` output:
- the input matrix in `fasta` format with amino acids re-coded to four amino acid classes represented by four nucleotide characters.