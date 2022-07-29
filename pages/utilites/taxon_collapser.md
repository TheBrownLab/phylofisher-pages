---
layout: default
title: taxon_collapser.py
parent: Utilities
nav_order: 16
permalink: /utilities/taxon_collapser
---

# `taxon_collapser.py`

Permanently combine taxa that have been added to the database

`taxon_collapser.py [OPTIONS] -i <input.tsv>`

Required arguments:
- `-i`, `--input to_collapse.tsv` A .tsv containing a Unique ID, higher and lower taxonomic designations, long name, and the Unique IDs of the taxa to collapse, for each chimera one per line.

Optional arguments:
- `-h`, `--help` Show this help message and exit.

`taxon_collapser.py` output:
- a new line in `metadata.tsv` with the information provided in the input .tsv.
- protein sequences for the new taxon in the corresponding ortholog and paralog fasta files in the database