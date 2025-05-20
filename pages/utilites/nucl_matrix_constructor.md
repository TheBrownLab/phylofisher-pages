---
layout: default
title: nucl_matrix_constructor.py
parent: Utilities
nav_order: 14
permalink: /utilities/nucl-matrix-constructor
---

# `nucl_matrix_constructor.py`

Create nucleotide super-matrix from orthologs

`nucl_matrix_constructor.py [OPTIONS]`

Required arguments:
-  `-i`, `--input <in_dir>` Path to `prep_final_dataset_<M.D.Y>`

Optional arguments:
- `-of`, `--out_format <format>`  Desired format of the output matrix.
    - Options: fasta, phylip (names truncated at 10 characters), phylip-relaxed (names are not truncated), or nexus.
    - Default: fasta
- `-t`, `--threads N` Desired number of threads to be utilized.
    - Default: 1
- `--clean_up` Clean up large intermediate files.
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./nucl_matrix_constructor_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

Default `nucl_matrix_constructor.py` output:
- a directory `nucl_matrix_constructor_out_<M.D.Y>` that contains:
  - a directory `cds` that contains:
    - {unique_id}.fas - a copy of the input nucleotide fasta file with headers renamed.
    - {unique_id}.fas.nin - an output file from `makeblastdb`
    - {unique_id}.fas.nhr - an output file from `makeblastdb`
    - {unique_id}.fas.nsq - an output file from `makeblastdb`
  - a directory `tblastn` that contains:
    - {gene_name}.{unique_id}.tsv - a tab separated file with the top tblastn hit.
  - a directory `nucl_seqs` that contains:
    - {gene_name}.fas - a FASTA file with the nucleotide sequences of the top tblastn hits.
  - a directory `logs` that contains:
    - a directory `makeblastdb` that contains:
      - {unique_id}.log - the log file from `makeblastdb`
    - a directory `tblastn` that contains:
      - {gene_name}.{unique_id}.log - the log file from `tblastn`
    - a directory `mafft` that contains:
      - {gene_name}.log - the log file from `mafft`
    - a directory `trimal` that contains:
      - {gene_name}.log - the log file from `trimal`
  - a directory `mafft` that contains:
    -  `{gene_name}.aln` - output of of MAFFT
  - a directory `trimal` that contains:
    - `{gene_name}.final` - output of trimAL. Trimmed alignments, in FASTA format, that will be used for concatenation.
  - `indices.tsv` - a tab separated file with three columns outlining the single gene boundaries in the supermatrix:
      1. Gene - name of the gene
      2. Start - first position of the gene within the super matrix
      3. Stop - last position of the gene within the super matrix
  - `occupancy.tsv` - a tab separated file with a column for each gene and a row for each taxon. This file details the presence or absence of each taxon for each gene represented by either a 1 or 0, respectively.
  - `matrix.<fas | nex | phy>` - the concatenated super matrix of all genes in the provided input directory in the specified file format
  - `matrix_constructor_stats.tsv` - a tab separated file with two columns:
    1. Taxon - Unique ID of taxon in the database
    2. Percent Missing Data - percentage of unoccupied sites within the concatenated matrix.
