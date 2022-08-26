--- 
layout: default
title: Single Gene Trees
parent: Introduction
nav_order: 7
permalink: /introduction/single-gene-trees
---

# Automated Filtering, Alignment, Trimming, and Single Gene Tree Construction

PhyloFisher also includes a python script `sgt_constructor.py` to automatically filter, align, trim, length filter, and construct phylogenetic trees from all homolog alignments. The script takes the output files from `fisher.py` (original single-protein alignments that now contain newly added sequences selected by the fisher algorithm for input taxa as well as the previously denoted paralogs from the database) and removes any dashes to produce an unaligned set of sequences for non-homologous character removal via PREQUAL v. 1.02 (Whelan et al., 2018) using the default settings. Next, a length filtering step is performed to minimize the inclusion of proteins predicted from fragments of the same gene. This is common in proteomes predicted from transcriptomes. First, sequences are aligned with the program MAFFT using the settings `–globalpair –maxiterate 1000 –unalignlevel 0.6`. This is followed by assessment of alignment error and uncertainty by the program Divvier v. 1.01 (Ali et al., 2019) using the options `-partial -mincol 4 -divvygap`. The resulting alignments are trimmed using BMGE v. 1.1.2 (Criscuolo and Gribaldo, 2010) with a gap-rate cutoff of 0.3. Any sequence whose length is less than half the total alignment length, after BMGE filtering, is removed. After removal of “short” sequences, files are prepared for single-protein phylogenetic tree construction by rerunning MAFFT and Divver as above, followed by trimming with the program trimAl with a gap threshold of 0.01. Finally, single-protein tree reconstruction is performed using RAxML v. 8.2.12 (Stamatakis, 2014) with the options `-m PROTGAMMALG4XF -f a -x 123 -N 100 -p 12345`. When single gene tree construction begins `sgt_constructor.py` will check to see how many gene trees are to be built and how many threads were provided by the user. If the number of gene trees to be built is greater than the number of threads provided, `sgt_constructor.py` will run as many jobs as it can using a single thread each. This process will continue until all gene trees have been built. If the total number of gene trees to be built is less than the number of threads available `sgt_constructor.py` will distribute all threads available as evenly as possible.