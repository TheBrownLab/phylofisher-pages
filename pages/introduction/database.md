---
layout: default
title: Database
parent: Introduction
nav_order: 5
permalink: /introduction/database
---

# PhyloFisher’s Provided Database

### PhyloFisher’s Provided Database Is...
The PhyloFisher package is equipped with a manually curated database of 240 protein coding genes from up to 304 eukaryotes that can be used for phylogenomic analyses of eukaryotic organisms. Details on the genes and taxa included in the database can be found currently at the below link. A metadata file (metadata.tsv) that provides information on the proteomes used in database construction is included with the database and can be found in the directory database/. In addition to a single ortholog of each of the databases’s 240 genes, a database of each gene’s paralogs is maintained.

### PhyloFisher’s Provided Database Is Not...
A set of genes that are universally present and single copy in all eukaryotic taxa included in the database.

### How a User’s PhyloFisher Database Changes Over Time
Regardless of whether a user chooses to utilize the provided database or their own custom database, the nature of the PhyloFisher workflow changes the chosen database overtime in a way that increases the database’s ability to inform a user on levels and phylogenetic location of paralogy for each gene in the database. Typically, the addition of new taxa to phylogenomic databases, especially underrepresented lineages, often reveals previously unknown or “hidden” paralogy. This previously unknown paralogy can exist at any level from shallow and species specific to ancient paralogy that simply could not be inferred with the previous database. Depending on the level of paralogy and the user’s phylogenetic question, accidental inclusion could have dramatic effects on phylogenomic inference and subsequent interpretations of evolutionary events based on the resulting phylogenomic tree. Once revealed, newly discovered paralogs are demarcated as such and maintained in the paralog portion of the database to aid in the identification of the paralog from newly added taxa in subsequent rounds of addition and prevent inclusion in future phylogenomic datasets. By continuously keeping a record of all known paralogs regardless of their emergence in evolutionary time a user’s decision regarding ortholog selection will always be the most informed even if/when the depth of their phylogenetic questions change over time. Our strategy also allows for the construction of a larger/more complete phylogenomic dataset as the most well represented orthologs can be chosen for phylogenomic analyses. 

Users do have the option of slimming down the database through complete deletion of taxa. User’s may also choose to exclude an organism and/or the organism’s paralogs from the working dataset used for single gene tree construction. While these options are provided to ease the computational burden of single gene tree construction, we highly recommend using as many taxa and their associated paralogs as feasible. Experience has shown that including more taxa will lead to more informed ortholog selection and therefore a more reliable final tree.