---
layout: default
title: Download Provided Dataset 
parent: Getting Started
nav_order: 2
permalink: /getting-started/download-provided-dataset/
---

# Download Provided Dataset

Download PhyloFisher’s Provided Database
1. Retrieve the provided starting database via wget:<br/>
 `wget https://ndownloader.figshare.com/files/29093409`
2. Uncompress the .tar.gz file:<br/>
 `tar -xzvf 29093409`

The uncompressed database directory contains the subdirectories and files detailed below.
- `database/`
  - `backups/`
    - `{Month}_{Day}_{Year}.tar.gz` a compressed file containing backups of the two database folders `orthologs/`, `paralogs/`, the database file `metadata.tsv`, and `tree_colors.tsv`
  - `datasetdb/`
    - `datasetdb.dmnd` a diamond database of the orthologs
    - `datasetdb.fasta` a fasta file of the orthologs used to construct the diamond database
  - `orthologs/`
    - `{gene_name}.fas` 240 fasta files of the orthologs
  - `orthomcl/`
    - `bacterial` abbreviated names of bacterial species present in OrthoMCL
    - `gene_og` a tsv file detailing the names of the 240 genes and their corresponding OrthoMCL orthogroup number(s)
    - `orthomcl.diamonddb.dmnd` diamond database of OrthoMCL
  - `paralogs/`
    - `{gene_name}_paralogs.fas` 240 fasta files of the paralogs
  - profiles
    - `{gene_name}.hmm` 240 profile hmm files of the orthologs
  - proteomes/
    - `{Unique_ID}.faa.tar.gz` complete proteomes of all taxa in the database
  - `metadata.tsv` tsv file of containing metadata for species in the database. Detailed extensively in the section “Detailed Explanation of the PhyloFisherDatabase_v1.0 Metadata File” of this manual
  - `tree_colors.tsv` a comma separated file used to color taxa based on taxonomy for manual inspection of single gene trees.