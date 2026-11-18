---
layout: default
title: plot_matrix_completeness.py
parent: Utilities
nav_order: 24
permalink: /utilities/plot-matrix-completeness
---

# `plot_matrix_completeness.py`

Plot the site-wise and gene-wise completeness of each taxon in a supermatrix.

`plot_matrix_completeness.py [OPTIONS] -i <matrix> -l <taxa_list> -g <gene_occupancy>`

Required arguments:
- `-i`, `--input <matrix>` Path to the supermatrix in FASTA format (e.g., `matrix.fas` from `matrix_constructor.py`)
- `-l`, `--taxa_list <taxa_list>` Path to a text file containing taxon names, one per line. Taxa are plotted from top to bottom in the order they appear in this file, so the order can be matched to a tree figure. Every taxon in the matrix must be listed.
- `-g`, `--gene_occupancy <gene_occupancy>` Path to a gene occupancy file (e.g., `occupancy.tsv` from `matrix_constructor.py`)

Optional arguments:
- `-h`, `--help` Show this help message and exit

Default `plot_matrix_completeness.py` output:
- `<matrix_basename>_completeness.pdf` - written to the current working directory. A horizontal bar chart showing two values for each taxon:
  - Site-wise completeness - the proportion of sites in the supermatrix that are not gaps
  - Gene-wise completeness - the proportion of genes in which the taxon is present
