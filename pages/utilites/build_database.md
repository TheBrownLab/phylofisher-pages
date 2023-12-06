---
layout: default
title: build_database.py
parent: Utilities
nav_order: 6
permalink: /utilities/build-database
---

# `build_database.py`

Construct a custom database or update taxonomy in a database.

`build_database.py [OPTIONS]`
Optional arguments:
- `-t`, `--threads <N>` Number of threads.
  - Default:1
- `-n`, `--no_og_file` Do not make Gene OG file.
- `-o`, `--og_threshold 0.X` (0-1) proportion of sequences that must hit an OrthoMCL orthogroup for the group to be assigned.
  - Default: 0.1 (10%)
- `--rename <to_rename.tsv>` Rename taxa in the database. Input is a tab-delimted file (.tsv) containing the Old Unique ID, New Unique ID, and New Long Name (Table 7).
- `-h`, `--help` Show this help message and exit.

**NOTE:** `build_database.py` must be run within `PhyloFisherDatabase_v1.0/database`

`build_database.py` output:
- a directory `profiles/` that contains:
  - profile HMMs of all ortholog files from the custom database.
- a directory `datasetdb/` that contains:
  - a diamond blast database of the orthologs from the custom database.
- a directory `paralogs/` - This empty directory is created if no paralogs directory exists initially.
- a tab separated file `gene_og` with two columns:
  1. Name of gene from the custom database.
  2. OrthoMCL orthogroup identification number(s) assigned to a gene from the custom database separated by commas.

What occurred:
- The script `build_database.py` will:
  - align the provided set of orthologs using MAFFT and create profile HMMs for each gene alignment using the `hmmbuild` utility from the HMMER3 package. These profiles will be used in the ortholog “fishing” algorithms implemented in `fisher.py`.
  - build a diamond blast database from the set of provided orthologs for use in the ortholog “fishing” algorithms implemented in `fisher.py`.
  - assign OrthoMCL orthogroup number(s) to each ortholog for use in the ortholog “fishing” algorithms implemented in `fisher.py`.
    - OrthoMCL orthogroup numbers are assigned by using all sequences in a provided gene file as queries in a BLAST search against the OrthoMCL v. 5.0 database. If a user defined percentage (default = 10%) of sequences hit an OrthoMCL orthogroup with a significance threshold of evalue < 1e -10 then that Orthogroup is assigned to the gene.
    - More than one OrthoMCL orthogroup numbers can be assigned to one gene.
    - If the provided gene alignment is assigned “no group” in OrthoMCL the gene cannot be used in the PhyloFisher workflow.
    - If the gene is assigned a bacterial OrthoMCL orthogroup the gene cannot be used in the PhyloFisher workflow.

**NOTE:** OrthoMCL orthogroup assignment hinges on integrity of ortholog choices in the starting ortholog files provided. If paralogs are unknowingly present in the provided ortholog alignments the paralogs will likely be prioritized by the fisher algorithm. To investigate the level of paralogy of genes in a custom database, we strongly recommend users re-add all taxa in their custom database using the main workflow of PhyloFisher. After an initial run through the main PhyloFisher workflow that includes manual curation, `build_dataset.py` will update profile HMMs, and blast databases to promote highest level of accuracy by the fisher algorithm in subsequent runs.

`build_dabase.py --rename`:
- The `--rename` flag allows users to rename taxa in the database. 
- `--rename` requires a tab-delimted file (.tsv) containing the Old Unique ID, New Unique ID, and New Full Name (Table 7).
- The script will back up the database and then do a full rebuild of the database which includes re-aligning, re-trimming, and rebuilding profile HMMs using the new name provided for each taxon in the input file.


| Old Unique ID | New Unique ID |    New Full Name    |
| :-----------: | :-----------: | :-----------------: |
|   Pleucart    |   Chrycart    | Chrysotila carterae |

<b>Table 7:</b> Example input file for the `--rename` flag of `build_database.py`. Here <i>Pleurochrysis carterae</i> (Unique
ID = Pleucart) is being renamed to <i>Chrysotila carterae</i> (Unique ID = Chrycart) in the database.
