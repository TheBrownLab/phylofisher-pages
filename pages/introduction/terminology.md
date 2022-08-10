---
layout: default
title: Terminology
parent: Introduction
nav_order: 4
permalink: /introduction/terminology
---

Terminology Used Throughout PhyloFisher Documentation 

Throughout this manual different collections/types of data are referred to using specific names in an attempt to provide clarity to the exact set of data being referenced (Figure 2).

The seven collections of data referenced in the manual are:

1. Database - the database is a collection of manually curated sequences demarcated as either orthologs or paralogs. This can refer to either the provided database or a custom database supplied by the user. Final decisions regarding orthology and paralogy made by a user during manual curation of sequences collected from newly input proteomes are stored here. The initial database provided has been manually curated prior to its release, however the application of different phylogenetic methods, manual curation practices, and taxon selection will cause the user’s database to change over time.

2. Working Dataset - the purpose of the working dataset is to aid in the identification of orthologs, paralogs, and contaminants from input proteomes. The working dataset is created when sequences are collected by fisher.py from input proteomes and appended to the copies of the corresponding homolog files from the database. These data will then move through the PhyloFisher workflow until final decisions based on manual curation have been applied to the database. A working dataset is not revisited after decisions from manual curation have been made and applied to the database.

3. Phylogenomic Dataset - A set of orthologs and taxa in the form of individual ortholog alignments and a concatenated matrix of these alignments that have been selected from the database to perform phylogenomic analyses on.
<figure>
    <img
        src="https://thebrownlab.github.io/phylofisher-pages/assets/images/Dataset_explanation_fig.png"
        height="75%"
        width="100%" 
        class="center"/>
    <figcaption>
        Figure 2: Flow chart of the PhyloFisher workflow documenting how collections of data are referenced throughout the manual.
    </figcaption>
</figure>

4. Gene(s) - The term gene is used throughout this manual to refer to a group of closely related homologs (similar to a gene family). These genes are named based on the corresponding human or Arabidopsis thaliana orthologs that were used as queries in BLAST searches to collect sequences from other eukaryotic organisms during the construction of the phylogenomic database developed in Tice et al., 2016. The aforementioned database was used as a starting point for construction of the PhyloFisher v1.0 database. We have chosen not to use either of the terms “gene family” or “orthogroup” because these genes only contain the most similar sequences to the initial search query rather than all potential members.

5. Ortholog(s) - The term ortholog, in the context of PhyloFisher, refers to a sequence(s) within the database that will ultimately be used for the construction of phylogenomic datasets. Additionally, the term ortholog is applied to the putative sequence from each newly added taxon that was selected by the fisher.py algorithm for use in phylogenomic datasets, pending decisions made during manual curation.

6. Paralog(s) - The term paralog, in the context of PhyloFisher, refers to sequences that are included in working datasets to enable proper ortholog selection and to reveal frequency of duplications in a particular gene and taxonomic group. The database's paralogs help users avoid the inclusion of sequences from different paralogs for different species and thus avoid phylogenetic signal derived from duplication events rather than speciation in the final phylogenomic analyses. Additionally, the term paralog refers to sequences that are collected from newly input taxa that were not selected by the fisher.py algorithm as the putative ortholog, pending decisions made during manual curation. They can also represent hidden contaminants or variants of the same contig (e.g. due to a retained intron(s)). After manual curation all sequences that are denoted as “paralogs” will be stored in the database to be utilized during manual curation of subsequent taxon additions.

7. Homolog(s) - The term homolog is used when referring to datasets that consist of both orthologs and paralogs (such as the working dataset), or to describe the relationship between orthologs and paralogs.