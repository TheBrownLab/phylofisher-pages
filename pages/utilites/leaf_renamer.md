---
layout: default
title: leaf_renamer.py
parent: Utilities
nav_order: 20
permalink: /utilities/leaf-renamer
---

# `leaf_renamer.py`

Rename leaves in a phylogenetic tree to match the long names in the PhyloFisher database.

This utility is useful when you have a tree with Unique IDs as leaf names and want to replace them with the full taxonomic names from the database metadata for better readability and presentation.

`leaf_renamer.py [OPTIONS] -d <database> -tr <tree> -o <output>`

Required arguments:
- `-d`, `--database <database>` Path to PhyloFisher database directory
- `-tr`, `--tree <input.tre>` Path to input tree file in Newick format
- `-o`, `--output <output.tre>` Output tree file name

Optional arguments:
- `-h`, `--help` Show this help message and exit

Default `leaf_renamer.py` output:
- A tree file with leaf names replaced from Unique IDs to their corresponding long names from the database `metadata.tsv` file

**NOTE:** If multiple taxa in the database have the same long name, the Unique ID will be appended to the long name to maintain uniqueness (e.g., `Homo_sapiens_Homosapi`).
