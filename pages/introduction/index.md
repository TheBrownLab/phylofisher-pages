---
layout: default
title: Introduction
nav_order: 2
has_children: true
permalink: /introduction
has_children: true
has_toc: false
---

# What is PhyloFisher?

PhyloFisher is a software package written in Python3 that can be used for the creation, analysis, and visualization of phylogenomic datasets that consist of protein sequences from eukaryotic organisms. Unlike many existing phylogenomic pipelines, PhyloFisher comes with a manually curated database of 240 protein coding genes from 304 eukaryotic taxa. However, the tool can be used to analyze any user-provided database. PhyloFisher is also equipped with a set of utilities to aid in running routine analyses performed during construction of or on constructed phylogenomic datasets and visualization of the results. If you use a component of PhyloFisher in your research, please [cite](https://thebrownlab.github.io/phylofisher-pages/how-to-cite).


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