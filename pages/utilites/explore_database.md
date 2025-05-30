---
layout: default
title: explore_database.py
parent: Utilities
nav_order: 8
permalink: /utilities/explore-database
---

# `explore_database.py`

Examine the composition of the database using taxonomic terms as search queries.

`explore_database.py [OPTIONS]`

Optional arguments:
- `-d`, `--database <db_dir>` Path to the database directory if `config.py` has not been run.
- `-t`, `--higher_taxonomy` Show higher taxonomy and number of taxa in each group in the database.
- `-l`, `--lower_taxonomy` Show lower taxonomy and number of taxa in each group in the database.
- `-r`, `--get_higher <HigherTax>` Return table with all taxa assigned the given higher taxonomy that displays the UniqueID, Long Name, Higher and Lower taxonomy, the number of orthologs, and the number of paralogs present in the database.
- `-w`, `--get_lower <LowerTax>` Return table with all taxa assigned the given lower taxonomy that displays the UniqueID, Long Name, Higher and Lower Taxonomy, the number of orthologs, and the number of paralogs present in the database.
- `-o`, `--get_org <UniqueID>` For the given Unique ID returns the Long Name, Higher and Lower Taxonomic Designation, Data Type, Orthologs (number present in the database for the taxon), Paralogs (number present in the database for the taxon), and the Accession.
- `--update_metadata` Update the metadata in the database with the latest information from a provided metadata TSV file.

`--update_metadata` TSV file format:
- The first line should contain the column headers: `Unique ID`, `Long Name`, `Higher Taxonomy`, `Lower Taxonomy`, `Data Type`, and `Source`.
- Each subsequent line should contain the corresponding values for each column, separated by tabs.


| Unique ID |       Long Name        | Higher Taxonomy | Lower Taxonomy | Data Type |      Source     |
|:---------:|:----------------------:|:---------------:|:--------------:|:---------:|:---------------:|
|  Crypparv | Cryptosporidium parvum |    Alveolata    |  Apicomplexa   |  Genomic  | GCF_000165345.1 |
 
 **Table 8:**  Example `update_metadata.tsv` file for the `--update_metadata` option. The first line is the header, and each subsequent line contains the Unique ID, Long Name, Higher Taxonomy, Lower Taxonomy, Data Type, and Source for each taxon to be updated.