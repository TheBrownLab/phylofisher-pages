---
layout: default
title: taxon_collapser.py
parent: Utilities
nav_order: 17
permalink: /utilities/taxon_collapser
---

# `taxon_collapser.py`

Permanently combine taxa that have been added to the database.

`taxon_collapser.py [OPTIONS] -i <input.tsv>`

Required arguments:
- `-i`, `--input to_collapse.tsv` A .tsv containing a Unique ID, long name, higher taxonomy, lower taxonomy, and a list of Unique IDs to collapse for each chimera with one on each line.

Optional arguments:
- `-h`, `--help` Show this help message and exit.

`taxon_collapser.py` output:
- a new line in `metadata.tsv` with the information provided in `to_collapse.tsv`.
- protein sequences for the new taxon in the corresponding ortholog and paralog fasta files in the database


| ChimeraID  |   Long Name  |  HigherTax  |  LowerTax  | UniqueID1,UniqueID2  |
| :--------: | :----------: | :---------: | :--------: |:-------------------: |

**Table 7:** Example input file for `taxon_collapser.py`, `to_collapse.tsv`. One chimera per line. The first column is the Unique ID of the chimera to be collapsed. The second column is the long name of the new taxon. The third column is the higher taxonomy of the new taxon. The fourth column is the lower taxonomy of the new taxon. The fifth column is a comma separated list of Unique IDs to collapse into the new taxon.