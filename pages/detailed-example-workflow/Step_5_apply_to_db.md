---
layout: default
title: Apply to Database
parent: Detailed Example Workflow
nav_order: 4
permalink: /detailed-example-workflow/step5-apply-to-database
---

# Apply to Database

To backup the database, add new taxa to the database, and implement all decisions made during manual curation with ParaSorter run:

`apply_to_db.py [OPTIONS] -i <input_directory> -fi <fisher_output_dir>`

Required arguments:
  - `-i`, `--input <in_dir>` Path to input directory containing parsed tsv labeled {gene_name}_parsed.tsv
  - `-fi`, `--fisher_dir <fisher_output_dir>` Path to initial fisher.py output directory

Optional arguments:
  - `-t`, `--threads <N>` Number of threads
  - `--to_exclude to_exclude.txt` Path to .txt file containing Unique IDs of taxa to exclude from dataset addition with one taxon per line
    - Example: 
      - Unique ID1
      - Unique ID2
  - `-h`, `--help` Show this help message and exit.

`apply_to_db.py` will first backup the current database/ directory and place the backup in `PhyloFisherDatabase_v1.0/database/backups`. Next, `apply_to_db.py` will append orthologs from input taxa to their corresponding gene files located in `PhyloFisherDatabase_v1.0/database/orthologs/`, append paralogs for input taxa to their corresponding gene files located in `PhyloFisherDatabase_v1.0/database/paralogs/`, and remove sequences marked for deletion. `apply_to_db.py` will update the binary matrix file `db_ortholog_occupancy.tsv` for newly added taxa based on decisions made during manual curation. The file `metadata.tsv` will also be updated with information provided for newly added taxa in `input_metadata.tsv`. Next, `apply_to_db.py` will rebuild the database so sequences from newly added taxa are present in the profile HMMs, the diamond database. This will allow orthologs from the newly added taxa to be used as specific queries in subsequent runs of addition. Finally, `apply_to_db.py` will copy the input proteome of all new taxa that are added to the database to `PhyloFisherDatabase_v1.0/database/proteomes/`.