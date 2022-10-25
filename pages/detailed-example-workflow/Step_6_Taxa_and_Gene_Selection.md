---
layout: default
title: Taxa and Gene Selection
parent: Detailed Example Workflow
nav_order: 6
permalink: /detailed-example-workflow/step6-Taxa-and-Gene_Selection
---

# Select Taxa and Orthologs to be Included in a Phylogenomic Dataset

To select taxa and orthologs to be included in the final phylogenomic dataset users can run the scripts `select_taxa.py` and `select_orthologs.py` respectively. Each will generate a .tsv file (contents explained below) that will serve to select either taxa or orthologs to include and both .tsv files are used as input for the script `prep_final_dataset.py` downstream.

NOTE: If all taxa and all orthologs in the database are to be included in the final phylogenomic dataset steps 1 and 2 are not necessary. Skip directly to step 3.


1. Select taxa for the final phylogenomic analyses:

    `select_taxa.py` [OPTIONS]

    Optional arguments:

    - `--to_exclude taxa_to_exclude.txt` Path to a  text file of groups or individual taxa to exclude from the final phylogenomic matrix

    - `--to_include taxa_to_include.txt` Path to a text file that will re-include groups or individual taxa

    - `--chimeras chimeras.tsv` Path to a .tsv file that contains a Unique ID, higher and lower taxonomic designations of the chimera, and the Unique IDs of the taxa in the database to collapse, for each chimera one per line (Table 4)

    - `-h`, `--help` Show this help message and exit

    Default `select_taxa.py` output:

     - a .tsv file `select_taxa.tsv` with five columns:

        1. Unique ID

        2. Higher Taxonomy

        3. Lower Taxonomy

        4. Completeness (percentage of orthologs) from the database present in the taxon

        5. Include in Subset

    - a plot showing completeness (number of orthologs) in each taxon. Groups of taxa are colored by level of completeness in increments of 10% (Figure 5).


    NOTE: Detailed explanation of to the `--to_exclude` and `--to_include` options and their input files:

    By default all taxa will be included. These options were designed to decrease the amount of manual manipulation of `select_taxa.tsv` generated in this first run of `select_taxa.py`. Both options take a file created by the user that has one column with an organism’s Unique ID or a taxonomic rank (higher or lower) from the metadata to be excluded or included in downstream steps. The options can be used individually or in conjunction with one another to implement decisions on taxa selection in an automated fashion. For example, if all taxa in the eukaryotic assemblage “Amoebozoa” are to be excluded from downstream phylogenomic analyses provide the `--exclude_taxa` option with a file (named anything) that contains “Amoebozoa” as the first entry of the column. This will result in all amoebozoans being marked as “no” in the “Include in Subset” column of `select_taxa.tsv` when it is generated. If a user wanted all amoebozoans excluded except *Dictyostelium discoideum* (Unique ID = Dictdisc) provide the `--exclude_taxa` option with a file (named anything) that contains “Amoebozoa” as the first entry of the column as before and the `--to_include` option with a file (named anything) with “Dictdisc” as the first entry of the column. This will result in all amoebozoans being marked as “no” in the “Include in Subset” column of `select_taxa.tsv` except *D*. *discoideum* which will be marked “yes.”


    NOTE: `--to_include` is not necessary it only serves to ease the burden of manual taxa selection in cases as outlined above. All taxa are marked to include by default so it is NOT necessary to provide `--to_include` with a list of all taxa you wish to include in downstream steps.

    NOTE: Decisions provided to `--to_include` will override decisions provided to `--to_exclude` so be
    cautious.

    Alternatively, all changes can be made manually by opening `select_taxa.tsv` and changing taxa designations from “yes” to “no".

    <table class="center">
        <tr>
            <td>BrevCHIM</td>
            <td>Obazoa</td>
            <td>Breviatea</td>
            <td>Brevanat</td>
            <td>Lenilimo</td>
            <td>Pygsbifo</td>
        </tr>
    </table>
        <figcaption>
            <b>Table 4:</b> Example input .tsv file for the `--chimera` option of `select_taxa.py`. Here a chimera will be made from three breviates in the database. The chimera will have the Unique ID ”BrevCHIM”, the higher taxonomy ”Obazoa”, the lower taxonomy ”Breviatea” and will be made from Brevanat (*Breviata anathema*), Lenilimo (*Lenisia limosa*), Pygsbifo (*Pygsuia biforma*).
        </figcaption>
    
    <figure>
        <img
        src="https://thebrownlab.github.io/phylofisher-pages/assets/images/select_taxa.png"
            height="75%"
                width="100%" 
                class="center"/>
            <figcaption>
                <b>Figure 5:</b> Plot produced by `select_taxa.py`. Taxa Unique IDs are shown at the bottom of the figure across the x-axis. The percentage of total orthologs present in a taxon (completeness) is shown on the y-axis. The total number of taxa is shown across the top of the figure on the x-axis. The bars are colored by level of completeness in increments of 10%. Legend explaining color coding is shown in the top right of the figure
            </figcaption>
    </figure>


2. Select orthologs to be included in the final phylogenomic dataset

    `select_orthologs.py [OPTIONS]`

    Optional arguments:
    - `--out_group out_group.txt` Path to text file containing out group taxa Unique IDs

    - `-n`, `--gene_number <N>` Number of genes for analysis

    - `-c`, `--percent_complete <N>` Threshold for percent completeness

    - `-h`, `--help` Show this help message and exit

    `select_orthologs.py` output:

    - a tsv file `select_orthologs.tsv` with three either three (default) or five columns:

        1. Ortholog - ortholog name

        2. Total Completeness - percentage of all taxa to be included in the final phylogenomic dataset the ortholog is present in.

        3. In-Group Completeness (only present if `--out_group` option is utilized) -percentage of In-group taxa only to be included in the final phylogenomic dataset the ortholog is present in.

        4. Out-Group Completeness (only present if `--out_group `option is utilized) - percentage of Out-Group taxa only to be included in the final phylogenomic dataset the ortholog is present in.

        5. Include in Subset

    - a plot showing completeness (number of taxa) of each gene. Groups of genes are colored by level of completeness in increments of 10% (Figure 6).

    <figure>
        <img
        src="https://thebrownlab.github.io/phylofisher-pages/assets/images/select_orthologs.png"
            height="75%"
                width="100%" 
                class="center"/>
            <figcaption>
                <b>Figure 6:</b> Plot produced by `select_orthologs.py`. Ortholog names are shown at the bottom of the figure across the x-axis. The percentage of total taxa present in an ortholog (completeness) is shown on the y-axis. The total number of genes is shown across the top of the figure on the x-axis. The bars are colored by level of completeness in increments of 10%. Legend explaining color coding is shown in the top right of the figure.
            </figcaption>
    </figure>


3. Collect orthologs and taxa to be included in the final phylogenomic dataset

    `prep_final_dataset.py [OPTIONS]`

    Optional arguments:

    - `-o`, `--output <out_dir>` Path to user-defined output directory

        - default `./prep_final_dataset_<M.D.Y>`

    - `-h`, `--help` Show this help message and exit

    Default `prep_final_dataset.py` output:

    - a directory `prep_final_dataset_<M.D.Y>` that contains:

        - a fasta file of each ortholog selected to be in the final phylogenomic dataset each containing only taxa selected to be in the final phylogenomic dataset.