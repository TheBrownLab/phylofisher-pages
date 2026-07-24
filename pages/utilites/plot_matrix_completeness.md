---
layout: default
title: plot_matrix_completeness.py
parent: Utilities
nav_order: 21
permalink: /utilities/plot-matrix-completeness
---

# `plot_matrix_completeness.py`

Generate a bar plot of site-wise and gene-wise matrix completeness for the taxa in the provided matrix file and gene occupancy file.

This utility creates a horizontal bar plot showing two types of completeness for each taxon:
- **Site-wise completeness**: Proportion of non-gap characters in the supermatrix
- **Gene-wise completeness**: Proportion of genes present in the dataset

The output helps identify taxa with low data coverage and assess the overall completeness of your phylogenomic matrix.

`plot_matrix_completeness.py [OPTIONS] -i <matrix> -l <taxa_list> -g <gene_occupancy>`

Required arguments:
- `-i`, `--input <matrix.fas|nex|phy>` Path to input supermatrix file
- `-l`, `--taxa_list <taxa.txt>` Path to text file containing taxa names (one per line)
- `-g`, `--gene_occupancy <occupancy.tsv>` Path to gene occupancy TSV file (e.g., `occupancy.tsv` from the PhyloFisher workflow)

Optional arguments:
- `-h`, `--help` Show this help message and exit

Default `plot_matrix_completeness.py` output:
- `<matrix_basename>_completeness.pdf` - A PDF file containing a horizontal bar plot with:
  - **Green bars** (Gene-wise): Proportion of genes present for each taxon
  - **Blue bars** (Site-wise): Proportion of non-gap characters in the supermatrix for each taxon
  - Reference lines at 0%, 50%, and 100% completeness
  - Taxa are plotted in the order provided in the taxa list file

**Note:** All taxa in the taxa list file must be present in both the matrix file and the gene occupancy file, or the script will raise an error.
**Note:** The taxa list should be ordered in the way you want the taxa to appear in the plot.
**Note:** If orienting your phylogenetic tree in FigTree, you can use the "Taxa" selection mode to copy the order of taxa from the tree and create a taxa list file (by pasting into a text file in a text editor) that matches the tree order for plotting matrix completeness.
