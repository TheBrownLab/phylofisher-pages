---
layout: default
title: Frequently Asked Questions
nav_order: 100
permalink: /frequently-asked-questions
---

# Frequently Asked Questions

### What operating systems does PhyloFisher run on?
All aspects of PhyloFisher can be installed and run on Linux and MacOS systems. Only ParaSorter can also be run on Windows.

### How do I report an issue with PhyloFisher?
Please report any errors on the [PhyloFisher GitHub Repository](https://github.com/TheBrownLab/PhyloFisher)

### Can I run PhyloFisher on my laptop?
All aspects of PhyloFisher will run on a laptop computer. However, more powerful computational resources are recommended for single gene tree construction and phylogenomic tree construction using a large database such as the one provided.

### How long does a typical PhyloFisher run take?
The length of time an entire run takes is dependent on the computational resources available.

### Can I use my own starting database?
Yes. PhyloFisher is compatible with phylogenomic databases other than the one provided. Go [here](https://thebrownlab.github.io/phylofisher-pages/getting-started/custom-database-prep/) for further instructions.

### How do I change the default color selection used for single gene tree visualization?
Simply change the color for taxa in tree_colors.tsv. New colors can be selected from [here](https://amoeba.msstate.edu/phylofisher/pdfs/svgcolors.pdf).

### Can I change the designation of orthologs and paralogs in the provided database?
Yes. The designation of sequences as orthologs or paralogs in the provided database is not fixed. These can be changed during manual inspection of single gene trees and the changes will be applied to the database in downstream steps.

### Can I delete taxa or genes from the provided database?
Yes. We have provided `purge.py` for permanent removal of taxa from the database. Permanent removal of genes would require re-building a custom database from only the desired genes. This is possible and instructions for constructing a custom database are provided [here](https://thebrownlab.github.io/phylofisher-pages/getting-started/custom-database-prep/). However, an easier solution could be to
simply not include the genes in final phylogenomic datasets via `select_orthologs.py`.

### Do I have to use the provided script for single gene tree construction?
No. If you prefer to use alternate strategies from trimming and single gene tree construction other than those implemented in `sgt_constructor.py` you can re enter the PhyloFisher workflow after you have constructed single gene trees with your preferred methodology. However, you must use a maximum likelihood approach for single gene tree construction in order for downstream aspects of PhyloFisher to work properly.