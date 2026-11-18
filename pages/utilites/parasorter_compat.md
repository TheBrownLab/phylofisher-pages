---
layout: default
title: parasorter_compat.py
parent: Utilities
nav_order: 23
permalink: /utilities/parasorter-compat
---

# `parasorter_compat.py`

Backwards compatibility between PhyloFisher v1 and ParaSorter2.

`parasorter_compat.py` has two modes. `to_sqlite` packages the output of `sgt_constructor.py` into a ParaSorter2 project database, taking the place of `forest.py` in [Tree Parsing](https://thebrownlab.github.io/phylofisher-pages/detailed-example-workflow/step4-tree-parsing). Once the gene trees have been inspected in ParaSorter2, `to_tsv` exports the saved decisions as the `{gene_name}_parsed.tsv` files read by `apply_to_db.py` in [Apply to Database](https://thebrownlab.github.io/phylofisher-pages/detailed-example-workflow/step5-apply-to-database).

## `to_sqlite`

Package `sgt_constructor.py` output into a ParaSorter2 project database.

`parasorter_compat.py to_sqlite [OPTIONS] -i <sgt_constructor_out_<M.D.Y>-local.tar.gz>`

Required arguments:
- `-i`, `--input <input>` Path to the `sgt_constructor_out_<M.D.Y>-local.tar.gz` file produced by `sgt_constructor.py`

Optional arguments:
- `-o`, `--output <out.sqlite>` Path to the project database to write
  - Default: `sgt_constructor_out_<M.D.Y>-local.sqlite` next to the input (`sgt_constructor_out_<M.D.Y>-local_1.sqlite`, `sgt_constructor_out_<M.D.Y>-local_2.sqlite`, ... when `-n` is greater than 1)
- `-n`, `--num_parsers <N>` Number of people parsing. Splits the genes into N databases with roughly equal numbers of tips to review, so the work of inspecting gene trees can be divided among several people.
  - Default: `1`
- `--force` Overwrite an existing project database. This discards any ParaSorter2 decisions saved in it.
- `-h`, `--help` Show this help message and exit

Default `parasorter_compat.py to_sqlite` output:
- `sgt_constructor_out_<M.D.Y>-local.sqlite` - a ParaSorter2 project database containing every gene tree (`{gene_name}.treefile`), its alignments (`{gene_name}.final`, `{gene_name}.trimmed`, and the untrimmed `{gene_name}.aln`), and the files `metadata.tsv`, `input_metadata.tsv`, and `tree_colors.tsv`

**NOTE:** ParaSorter2 builds the merged sequence of a concatenation group from the untrimmed alignments. These are included in `-local.tar.gz` files written by `sgt_constructor.py` v1.3.0 and later (`{gene_name}.untrimmed`). For tarballs from earlier versions, `to_sqlite` looks for the untrimmed alignments in the `mafft` directory of the `sgt_constructor_out_<M.D.Y>` directory next to the tarball. If neither is available, concatenation groups cannot be exported by `to_tsv`.

## `to_tsv`

Export the decisions saved in ParaSorter2 as `{gene_name}_parsed.tsv` files for `apply_to_db.py`.

`parasorter_compat.py to_tsv [OPTIONS] -i <project.sqlite> [<project.sqlite> ...]`

Required arguments:
- `-i`, `--input <project.sqlite> [<project.sqlite> ...]` Path(s) to the ParaSorter2 project database(s), e.g., every database written by `to_sqlite -n`

Optional arguments:
- `-o`, `--output <out_dir>` Directory to write `{gene_name}_parsed.tsv` files to
  - Default: `./parasorter_out_<M.D.Y>`
- `-fi`, `--fisher_dir <fisher_dir>` Path to the `fisher.py` output directory the project was built from. Required if the project contains concatenation groups.
- `-fo`, `--fisher_out <fisher_out>` Where to write the copy of `<fisher_dir>` with the merged sequences of concatenation groups added
  - Default: `<out_dir>/fisher_out`
- `-h`, `--help` Show this help message and exit

Default `parasorter_compat.py to_tsv` output:
- a directory `parasorter_out_<M.D.Y>` that contains:
  - `{gene_name}_parsed.tsv` - the ortholog (`o`), paralog (`p`), and delete (`d`) decisions saved in ParaSorter2 for each gene, to be provided to `apply_to_db.py` via `-i`
  - a directory `fisher_out` (only when `-fi` is given) - a copy of the `fisher.py` output with the merged sequence of each concatenation group added to its gene's `.fas` file, to be provided to `apply_to_db.py` via `-fi`

**NOTE:** Each concatenation group is exported as a single new sequence tagged with the group's decision, and its member sequences are marked for deletion.

**NOTE:** Only genes with saved (Parsed) decisions are exported. Genes that have not been reviewed are skipped, and a gene reviewed in more than one of the input databases is reported as a conflict and not exported.
