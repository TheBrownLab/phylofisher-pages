---
layout: default
title: Utilities
nav_order: 4
permalink: /utilities
has_children: true
has_toc: false
---

# Utilities
## Overview
While the above processes will allow users to develop a phylogenomic dataset and infer single gene and phylogenomic trees using whatever best practices are available to them, many more analyses are often used to examine the effects of aspects of the data. Phylogenomic analyses are often accompanied by additional analyses in which users manipulate their phylogenomic dataset or examine the dataset in a different fashion to reveal artifacts in their data. Here we provide users with simple programs to perform some of the most often employed tactics.

[`aa_comp_calculator.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/aa-comp-calculator): Calculates amino acid composition and uses euclidean distances to hierarchically cluster these data, in order to examine if amino acid composition may bias the groupings that were inferred in a phylogenomic tree. See Brown et al., 2018 for an example.

[`astral_runner.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/astral-runner): Generates input files and infers a coalescent-based species tree given a set of single ortholog trees and bootstrap trees using ASTRAL-III (Zhang et al., 2018).

[`backup_restoration.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/backup-restoration): Restores a previous version of the database from the directory backups/.

[`bipartition_examiner.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/bipartition-examiner): Calculates the observed occurrences of clades of interest in bootstrap trees.

[`build_database.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/build-database): used to format custom databases for use in the PhyloFisher workflow. This utility is also used to rename taxa in either the provided database or a custom database.

[`explore_database.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/explore-database): Used to examine the composition of the database using taxonomic terms as search queries.

[`fast_site_remover.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/fast-site-remover): The fastest evolving sites are expected to be the most prone to phylogenetic signal saturation and systematic model misspecification in phylogenomic analyses. This tool will remove the fastest evolving sites within the phylogenomic supermatrix in a stepwise fashion, leading to a user defined set of new matrices with these sites removed.

[`fast_taxa_remover.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/fast-taxa-remover): Removes the fastest evolving taxa, based on branch length. This tool will remove the fastest evolving taxa within the phylogenomic supermatrix in a stepwise fashion, leading to a user defined set of new matrices with these taxa removed.

[`genetic_code_examiner.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/genetic-code-examiner): Checks stop-to-sense and sense-to-sense codon reassignment signal in transcriptome/genome data. This script is using the advantage of the phylogenetically broad database accompanying our software. The first step is the creation of multiple sequence alignments from all fasta files containing manually curated orthologous sequences. This step can take some time but it is necessary only for the first run of genetic_code.py. In the next step, tblastn searches with orthologs from selected related organism/s in the database are performed against the given transcriptome/genome (with 1e-30 default e-value). For all genes, the best scoring hit is investigated for “good quality positions”. Such positions are located at least 6 amino acids from the beginning or end of the blast alignment and the number of low scoring mismatches (normally denoted by spaces in blast middle line) in close proximity to these positions (+- 3 amino acids) is less than 3. Corresponding positions from the query are then analyzed in previously prepared multiple sequence alignments and information about
well-conserved amino acids (in more than 70% of organisms, default) is collected and connected to the underlying codon from transcriptome/genome. Codons which show evidence for signals different from the standard genetic code signal are then visualized in the form of bar plots (occurrence of conserved amino acids). Thanks to the evolutionary well-conserved nature of proteins in our database, realigning all sequences again with provided input nucleotide data is not necessary. This script performs well with
genomic and transcriptomic data. Analysis of one transcriptome/genome should usually take less than 5 minutes on an average personal computer. It has to be mentioned that alternative genetic code signal from multiple sequence alignments is only one way to analyze this phenomenon and tRNAs should be investigated as well if possible.

[`heterotachy.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/heterotachy): Within-site rate variation (heterotachy) (Lopez et al., 2002) has been shown to cause artificial relationships in molecular phylogenetic reconstruction (Inagaki et al., 2004). This tool will remove the most heterotachious sites within a phylogenomic supermatrix in a stepwise fashion, leading to a user defined set of new matrices with these sites removed.

[`mammal_modeler.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/mammal-modeler): Generates a MAMMaL site heterogeneous model from a user input tree and
supermatrix with estimated frequencies for a user defined number of classes. This program creates a set of temporary files from the user provided input that MAMMaL is able to handle. The output is a heterogeneous model in Nexus format that is usable in IQtree using options (-m LG+ESmodel+G -mdef esmodel.nex). This program outputs by default a 61 class mixture model with 60 site frequency classes and the overall amino acid frequencies (+F) of the phylogenomic dataset. Also please note that when using this program we hard-code the “not using likelihood weighting” option. This is because using likelihood weighting will cause issues in the calculation of likelihood weights in sparse phylogenomic matrices. The problem is that there may be pairs of sequences that have no sites in common. Specifically, the proportion of times an amino acid occurs for the pair of sequences becomes NA because the denominator is 0 (calculation is [p_{aa;sj}] in Eqn (5) of the Susko et al., 2018) (Ed Susko personal communication).

[`purge.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/purge): This tool is used for deleting taxa and/or taxonomic groups from the database and metadata permanently.

[`random_resampler.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/random_resampler): This tool randomly resamples the gene set into a set of new matrices that are subsamples of the super matrix. It constructs supermatrices from randomly sampled genes with user defined options such as the confidence interval sampling all genes in a random fashion and the percentage of subsampling a user requires per sampling step. This method was used in Brown et al., 2018 as an example.

[`rtc_binner.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/rtc_binner): Calculates the relative tree certainty score (RTC) in RAxML Stamatakis, 2014 of each single ortholog tree and bins them based on their RTC scoring into top 25%, 50%, and top 75% sets. Supermatrices are constructed from these bins of orthologs.

[`SR4_class_recoder.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/SR4_class_recoder): To minimize phylogenetic saturation this tool recodes input supermatrix into the four-character state scheme of SR4 (Susko and Roger, 2007), based on amino acid classification.

[`taxon_collapser.py`](https://thebrownlab.github.io/phylofisher-pages/utilities/taxon_collapser): Allows users to combine multiple operational taxonomic units into one single taxon. For example if a user has multiple single cell libraries from a taxon or multiple strains of the same species (or genus etc.), a user may decide to collapse all these strains/libraries into a single taxon.