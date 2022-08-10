---
layout: default
title: Contents
parent: Introduction
nav_order: 3
permalink: /introduction/contents
---

# PhyloFisher Package Contents
- Manually curated database of 240 orthologs and their paralogs from 304 eukaryotic taxa. These taxa cover the known diversity of eukaryotes.
- Main Workflow tools for:
  - The preparation of custom databases composed of protein coding genes in lieu of the provided database
  - Ortholog and paralog “mining” from input proteomes
  - Evaluating completeness in the database of newly input data
  - Automated removal of non-homologous sites, alignment, trimming, length filtering and single gene tree construction
  - Visualization of single gene trees and interactive selection of orthologs, paralogs, and removal of contamination
  - Generation of final statistics post ortholog selection and contamination removal
    - Can be subset by user provided thresholds of completeness or by assigned taxonomy.
  - Creation of chimeric taxa for use in phylogenomic analyses
  - Automated concatenation of phylogenomic matrices
- Utilities for:
  - Alternative genetic code prediction
  - Compositional bias testing (amino acid re-coding)
  - The removal of fast evolving sites from a phylogenomic dataset
  - The removal of fast evolving taxa from a phylogenomic dataset
  - Detection and removal of the most heterotachious sites in a phylogenomic dataset
  - Examining the number of occurrences of clades of interest in bootstrap trees
  - Matrix construction from randomly re-sampled genes from a phylogenomic dataset
  - Binning single-protein trees based on Relative Tree Certainty (RTC)
  - collapsing of multiple proteomes to produce a single “most complete” proteome with regards to the database (useful for single-cell data and to form chimeric taxa from closely related species)

<br><br>
<figure>
    <img
        src="https://thebrownlab.github.io/phylofisher-pages/assets/images/Figure1_general_workflow-EDITED5.png"
        height="75%"
        width="100%" 
        class="center"/>
    <figcaption>
        Figure 1: Overview of the PhyloFisher workflow and package contents. The PhyloFisher package consists of a manually curated database of 240 protein coding genes and their paralogs from 304 eukaryotic taxa; a series tools to perform the essential steps of phylogenomic dataset construction (homolog collection, single-protein tree construction, removal of paralogs and contaminants, matrix concatenation); and many pre and post-construction analyses necessary for a publication-quality phylogenomic study.
    </figcaption>
</figure>