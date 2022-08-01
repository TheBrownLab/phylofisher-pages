---
layout: default
title: aa_comp_calculator.py
parent: Utilities
nav_order: 1
permalink: /utilities/aa-comp-calculator
---

# `aa_comp_calculator.py`

Calculate the amino acid composition of an input matrix.

`aa_comp_calculator.py [OPTIONS] -i <input_matrix>`

Required arguments:
- `-i`, `--input matrix` Path to input matrix for analysis

Optional arguments:
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./aa_comp_calculator_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

Default `aa_comp_calculator.py` output:
  - a directory `aa_comp_calculator_output_<M.D.Y>` that contains:
  - a tab separated file `aa_comp.tsv` with 21 columns:
    - “Taxon” - short name of taxon in dataset
    - Each of the following 20 columns are labeled with the IUPAC single letter abbreviation for each standard amino acid. The values in rows are the proportion of the corresponding amino acid in the sequence data for a taxon in the input file.
  - `AA_Composition_Hierarchical_Clustering.pdf` - a dendrogram built using pairwise distances calculated by Ward’s criterion between taxa after hierarchical clustering based on amino acid composition in pdf format Figure 7.

<figure>
    <img
        src="https://thebrownlab.github.io/phylofisher-pages/assets/images/aa_comp_calculator.png"
        height="75%"
        width="100%" 
        class="center"/>
    <figcaption>
        Figure 7: Plot produced by aa_comp_calculator. The plot is built using pairwise distances calculated by Ward’s criterion between taxa after hierarchical clustering based on amino acid composition as performed in Brown et al., 2018. Leaves are labeled and colored according to higher taxonomy of taxa in the provided alignment.
    </figcaption>
</figure>


