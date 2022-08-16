---
layout: default
title: Metadata Explanation
parent: Getting Started
nav_order: 5
permalink: /getting-started/metadata-explanation/
---

# Metadata Explanation

The file `metadata.tsv` initially contains information regarding the data used to construct the database.
As users add taxa to the database `metadata.tsv` acts as a permanent archival file and is updated after each
round of addition of new taxa.
The contents of `metadata.tsv` can be explored using the provided utility “explore_database.py”. A user
should never be required to manually open this file to view its contents. However, the structure of `metadata.tsv`
is detailed below.

- `metadata.tsv` is a tab delimited file with six columns:
  1. Unique ID - an abbreviated name for each taxon. We have followed an eight-letter convention. For user’s making a `metadata.tsv` for a custom database,Unique IDs cannot cannot contain underscores “_”, at symbols “@”, double dots 
  2. Long Name - Full name of the input taxon. For user’s making a `metadata.tsv` for a custom database, the long name cannot cannot contain underscores “_”, at symbols “@”, double dots “..”.
  3. Higher Taxonomy - The highest taxonomic rank for the input organism desired. We have chosen to use the “supergroup” level here but any user defined rank is accepted. However, we do recommend users choose a highly inclusive taxonomic rank here (phylum or class level in Linnaean terms) to promote the best possible performance of the fisher algorithm and other downstream tools.
  4. Lower Taxonomy - a taxonomic rank above the genus level for the input taxon
     - Notes on Taxonomy: The default taxonomic terms in `metadata.tsv` can be replaced with user preferred terms. If terms are to be replaced though, we recommend replacing them with synonyms of similar rank. DO NOT MIX SYNONYMOUS TERMS (see example below). This will lead to misbehavior in the fisher algorithm and wrongly denoted suspicious clades during generation of files for visualisation and manual inspection of single gene trees. The same erratic behavior will likely occur if our chosen taxonomic ranks are split up and replaced by several less inclusive taxonomic terms.
        - Example Taxonomic Change: If the term “Chromist” is preferred over “Stramenopiles”
        replace all instances of “Stramenopiles” in `metadata.tsv` with “Chromist” before adding
        new taxa with “Chromist” chosen as the higher taxonomic term in `input_metadata.tsv`.
        DO NOT MIX THE TWO, erratic behavior will ensue. Go here for more information
        regarding `input_metadata.tsv` requirements related to `metadata.tsv`.
  5. Data Type - A place to add a note about the type of data being added (ex. transcriptomic, genomic, EST . . .
  6. Source - A place to add notes about the source of the data such as accession numbers, “in-house information”, strain information etc.

**NOTE**: COMMA (,) MAY NOT BE USED ANYWHERE IN `METADATA.TSV`!