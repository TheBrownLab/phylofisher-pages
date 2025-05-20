---
layout: default
title: purge.py
parent: Utilities
nav_order: 14
permalink: /utilities/purge
---

# `purge.py`

Delete taxa and/or taxonomic groups from the database and `metadata.tsv`.

`purge.py [OPTIONS] -i to_purge.txt -d path/to/database`

Required arguments:
- `-i`, `--input <to_purge.txt>` Path to text file containing Unique IDs and/or Taxonomic designations of organisms for deletion
- `-d`, `--database <input_dir>` Path to database to purge

Optional arguments:
- `-h`, `--help` Show this help message and exit