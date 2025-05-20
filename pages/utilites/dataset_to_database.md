---
layout: default
title: dataset_to_database.py
parent: Utilities
nav_order: 7
permalink: /utilities/dataset-to-database
---

# `dataset_to_database.py`

Convert an existing PhyloFisher database to the new SQLite database format. This is required for version 2.0+ of PhyloFisher.

`dataset_to_database.py [OPTIONS]`

Required arguments:
- `-i`, `--input <db_dir>` Path to directory containing an existing PhyloFisher v1 database.

Optional arguments:
- `-o`, `--output` Path to user-defined output directory.
    - Default: `./dataset_to_database_<M.D.Y>`

`dataset_to_database.py` output:
- a directory called `./dataset_to_database_<M.D.Y>` with:
  - `phylofisher.db` - an SQLite database file containing metadata, sequence data, taxonomic data, and gene data.
  - `orthomcl/` - a directory containing the orthomcl files:
    - `orthomcl.diamonddb.dmnd` - a diamond database of OrthoMCL.
    - `gene_og` - a tsv file detailing the names of the 240 genes and their corresponding OrthoMCL orthogroup number(s).
    - `bacterial` - abbreviated names of bacterial species present in OrthoMCL.
  - `proteomes` - a directory containing the proteomes of the taxa in the database.
  - `nucleotides` - a directory containing the CDSs of the taxa in the database.
  - `profiles` - a directory containing hmm profiles of the genes in the database. 