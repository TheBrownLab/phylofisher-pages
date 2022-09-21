---
layout: default
title: fast_taxa_remover.py
parent: Utilities
nav_order: 8
permalink: /utilities/fast-taxa-remover
---

# `fast_taxa_remover.py`

Remove the fastest evolving taxa from a matrix based on branch length.

`fast_taxa_remover.py [OPTIONS] -m <input_matrix> -tr <input_tree>`

Required arguments:
- `-m`, `--matrix <matrix.fas|nex|phy>` Path to input matrix.
- `-tr`, `--tree <tree>` Path to input tree.
- `-i`, `--iterations <N>` Number of iterations.
-` -or`, `--ortholog_files` Path to directory containing the individual ortholog files. This will be the path to `prep_final_dataset_<M.D.Y>` if used within the main PhyloFisher workflow.

Optional arguments:
- `-in_format <format>` Input matrix format.
  - Options: `fasta`, `phylip` (names truncated at 10 characters), `phylip-relaxed` (names are not truncated), or `nexus`.
  - Default: `fasta`
- `-out_format <format>` Desired output format.
  - Options: `fasta`, `phylip` (names truncated at 10 characters), `phylip-relaxed` (names are not truncated), or `nexus`.
  - Default: `fasta`
- `-s`, `--step_size <N>` Number taxa removed per iteration.
  - Default: 1
- `-o`, `--output <out_dir>` Path to user-defined output directory.
  - Default: `./fast_taxa_removal_out_<M.D.Y>`
- `-t`, `--threads <N>` Desired number of threads to be utilized.
  - Default: `1`
- `-h`, - Show this help message and exit.

`fast_taxa_remover.py` output:
- a directory called `./fast_taxa_remover_out_<M.D.Y>` with sub-directories:
  - `steps_<N>` (N=step size) that contain:
- a directory `prequal` that contains:
  - `{gene_name}.aa` - unaligned gene file used as PREQUAL input.
  - `{gene_name}.aa.filtered` - output of PREQUAL. Used as input for MAFFT in subsequent length filtration step.
  - `{gene_name}.aa.filtered.PP` - output of PREQUAL.&
  - `{gene_name}.aa.warning` - output of PREQUAL.&
- a directory `mafft` that contains:
  - `{gene_name}.aln` - output of MAFFT and input for Divvier.
- a directory `divvier` that contains:
  - `{gene_name}.aln.partial.fas` - output of Divvier and input for timAl.
  - `{gene_name}.aln.PP` - output of Divvier.&&
- a directory `trimAl` that contains:
  - `{gene_name}.gt80trimAl` - output of trimAl. Trimmed alignments that will be used for concatenation.
- `indices.tsv` - a tab separated file with three columns outlining the single gene boundaries in the supermatrix. These columns are:
  1. Gene - name of the gene.
  2. Start - first position of the gene within the super matrix.
  3. Stop - last position of the gene within the super matrix.
- `matrix.<fas|nex|phy>` - the concatenated super matrix of all genes in the provided input directory in the specified file format.
- `matrix_constructor_stats.tsv` - a tab separated file with two columns:
  1. Taxon -Unique ID of taxon in the database.
  2. Percent Missing Data - percentage of unoccupied sites within the concatenated
matrix.

& - These are standard PREQUAL output files for each gene that PhyloFisher has appended the corresponding gene name to. See the [PREQUAL documentation](http://amoeba.msstate.edu/phylofisher/pdfs/prequal.pdf) for a thorough explanation of their contents.

&& - These are standard Divvier output files for each gene that PhyloFisher has appended the corresponding gene name to. See the [Divvier documentation](http://amoeba.msstate.edu/phylofisher/pdfs/divvier.pdf) for a thorough explanation of their contents.