---
layout: default
title: Matrix Construction
parent: Detailed Example Workflow
nav_order: 7
permalink: /detailed-example-workflow/step7-matrix-construction
---

# Matrix Construction

Trim, align, and concatenate orthologs into a super-matrix.

To do this run:
`matrix_constructor.py [OPTIONS] -i <input_directory>`

Required arguments:
  - `-i`, `--input <in_dir>` Path to `prep_final_dataset_<M.D.Y>`

Optional arguments:
  - `-f`, `--out_format <format>` Desired format of the output matrix
    - Options: `fasta`, `phylip`, `phylip-relaxed`, or `nexus`.
    - Default: `fasta`
  - `-if`, `--in_format <format>` format of the input files.
    - Options: `fasta`, `phylip`, `phylip-relaxed`, or `nexus`.
    - Default: `fasta`
  - `-c`, `--concatenation_only` Only concatenate alignments. Filtering, alignment, and trimming are not performed automatically.
  - `-t`, `--threads <N>` Desired number of threads to be utilized.
    - Default: `1`
  - `-o`, `--output <out_dir>` Path to user-defined output directory
    - Default: `./matrix_constructor_out_<M.D.Y>`
  - `-p`, `--prefix <prefix>` Prefix of input files
    - Default: `None`
    - Example: `path/to/input/prefix*`
  - `-s`, `--suffix <suffix>` Suffix of input files
    - Default: `None`
    - Example: `path/to/input/*suffix`
  - `-h`, `--help` Show this help message and exit

Default `matrix_constructor.p`y output:
  - a directory called `matrix_constructor_out_<M.D.Y>` containing:
    - a directory `prequal` that contains:
      - `{gene_name}.aa` - unaligned gene file used as PREQUAL input
      - `{gene_name}.aa.filtered` - output of PREQUAL. Used as input for MAFFT in subsequent length filtration step.
      - `{gene_name}.aa.filtered.PP` - output of PREQUAL.&&
      - `{gene_name}.aa.warning` - output of PREQUAL.&&
    - a directory `mafft` that contains:
      - `{gene_name}.aln` - output of of MAFFT and input for Divvier.
      - `{gene_name}.aln.PP` - output of PREQUAL.&&
    - a directory `divvier` that contains:
      - `{gene_name}.aln.partial.fas` - output of Divvier and input for timAl.
    - a directory `trimAl` that contains:
      - `{gene_name}.gt80trimAl.fas` - output of trimAl. Trimmed alignments, in FASTA format, that will be used for concatenation.
    - `indices.tsv` - a tab separated file with three columns outlining the single gene boundaries in the supermatrix:
      1. Gene - name of the gene
      2. Start - first position of the gene within the super matrix
      3. Stop - last position of the gene within the super matrix
    - `matrix.<fas | nex | phy>` - the concatenated super matrix of all genes in the provided input directory in the specified file format
    - `matrix_constructor_stats.tsv` - a tab separated file with two columns:
      1. Taxon -Unique ID of taxon in the database
      2. Percent Missing Data - percentage of unoccupied sites within the concatenated matrix.

&& - These are standard PREQUAL output files for each gene that PhyloFisher has appended the corresponding gene name to. See the PREQUAL documentation for a thorough explanation of their contents.