---
layout: default
title: Tree Parsing
parent: Detailed Example Workflow
nav_order: 4
permalink: /detailed-example-workflow/step4-tree-parsing
---

# Manual Inspection of Gene Trees

1. Render .svg and .tsv files of gene trees for visualization with ParaSorter

    If working on a remote server, copy the file `sgt_constructor_out_<M.D.Y>-local.tar.gz` file to your local
    machine for input into `forest.py`.

    `forest.py [OPTIONS] -i <input>`

    Required arguments:

    - `-i`, `--input <input_dir>` path to `sgt_constructor_out_<M.D.Y>-local.tar.gz`

    Optional arguments:

    - `-a`, `--contaminants <contams.tsv>` Path to file containing known contaminants to be removed. See Table 2

    - `-b`, `--backpropagate` Path to file containing known contaminants to be backpropagated. See Table 2

    - `-t`, `--threads <N>` Number of threads
    
        - Default: 1

    - `-o`, `--output <out_dir>` Path to user-defined output directory

        - Default: `./forest_out_<M.D.Y>`

    - `--local_run` To be used when `sgt_constructor_out.<M.D.Y>-local.tar.gz` has been downloaded from a server for single gene tree visualizations to be rendered locally.

    - `-h`, `--help` Show this help message and exit

    Default forest.py output:

    - a directory `forest_out_<M.D.Y>` that contains:

        - {gene_name}_tree.svg

        - {gene_name}.tsv


    If a user has *a priori* knowledge of eukaryotic contamination in their data they can provide
    `forest.py` with a file via the --contaminants flag. The file should be tab delimited and have three
    columns. In the first column is the Unique ID of the contaminated input proteome and in the second
    column the taxonomic term of the contaminant. Any of the three taxonomic levels used in PhyloFisher
    (higher taxonomy, lower taxonomy, Unique ID) can be used to identify contamination. Finally
    in the third column is the name of the taxonomic level chosen for the contaminant. See Table 2.
    When this file is provided, `forest.py` will pre-mark instances of this branching pattern for deletion
    regardless of MLBS for the relationship.

    If during manual curation of single gene trees a user discovers previously unknown pervasive
    contamination, rather than having to manually mark each instance for deletion, the user can
    provide `forest.py` with a file also in the format of Table 2 only with both the `--contaminants` and
    `--backpropagate` flags provided to `forest.py`. When the `--backpropagate` is added all decisions made in previously
    manually curated gene trees will be maintained rather than rewriting the original .tsv files with
    the only difference being the defined contaminant is marked for deletion.


    NOTE: Only sequences from newly added organisms can be pre-marked for contamination or
    have contamination back propagated. Contamination from previously added organisms must be
    marked manually if found after their initial addition.

    <br>

    | Dermalge | Chloroplastida | Higher Taxonomy |
    |:--------:|----------------|-----------------|

    **Table 2:** Example input file to premark or backpropagate known eukaryotic
    contaminants. Here *Dermamoeba algensis* (Unique ID = Dermalge) is contaminated
    with a eukaryote that is a member of Cholorplastida. Cholorplastida’s rank in
    PhyloFisher’s default metadata file is “Higher Taxonomy”

    <br>

    The file “tree_colors.tsv” is used by `forest.py` to color taxa by taxonomic rank when rendering .svg
    files of homolog for visualization via the included tool `ParaSorter`. A default tree_colors.tsv is
    supplied with the database. The default file is configured to have all taxa in the database colored by
    the higher taxonomic rank assigned to them in metadata.tsv which can be examined using `explore_database.py`

    <br>


    |      Taxonomy     |       Color       |
    |:-----------------:|:-----------------:|
    |     Amoebozoa     |        Red        |
    |   Ancyromonadida  |    LightSalmon    |
    |       CRuMs       |       Salmon      |
    |      Discoba      |        Gold       |
    |   Malawimonadida  |       Orange      |
    |     Metamonada    |     DarkViolet    |
    |       Obazoa      |      Crimson      |
    |      Rhizaria     |      Magenta      |
    |     Rhodophyta    | MediumSpringGreen |
    |   Stramenopiles   |  MediumSlateBlue  |
    |      Haptista     |   MediumSeaGreen  |
    |     Cryptista     |       Olive       |
    | Hemmimastigophora |   LavenderBlush   |
    |     Telonemia     |     MistyRose     |
    |   Chloroplastida  |    GreenYellow    |
    |     Alveolata     |    DeepSkyBlue    |
    |    Glaucophyta    |     LimeGreen     |
    |    Rhodelphidia   |    SpringGreen    |
    |      Alveida      |       Khaki       |
    |      Picozoa      |        Lime       |

    **Table 3**: Default tree_colors.tsv file. Color and the taxonomic rank that taxa are colored by can
    be changed by the user.

    <br>

    The color and the taxonomic rank that taxa are colored by can be changed by the user in the default
    file or users can provide config.py with an alternative tree_colors.tsv file. Taxa can be colored by any
    of the three possible taxonomic designations used in PhyloFisher; higher taxonomy, lower taxonomy,
    or by the taxon’s Unique ID. A lower taxonomic rank and the color assigned to it will take precedence
    over the higher taxonomic rank and its associated color that the lower taxonomic rank is a part of.
    For example, *Dermamoeba algensis* is assigned the higher taxonomic rank Amoebozoa, the lower
    taxonomic rank Discosea, and has the Unique ID “Dermalge” in metadata.tsv. By default, all members
    of Amoebozoa are colored red. However, if a user were to add “Discosea Brown” to “tree_colors.tsv”
    then all members of Discosea will be colored brown while all members of the other two sub lineages of
    Amoebozoa will remain red. If a user also added “Dermalge Teal” to “tree_colors.tsv” all members of
    Discosea will be colored brown except *D*. *algensis* which will be colored teal while all other amoebozoans
    will remain red.


    If a taxon was added that has a taxonomy not previously represented in the file metadata.tsv users
    will need to add one of the taxonomic ranks they assigned to the taxon in “input_metadata.tsv” or
    the organism’s Unique ID for the taxon to be colored by and a corresponding color to tree_colors.tsv.
    Users need to do this after the taxon has been added to the database so during subsequent rounds of
    addition and single gene tree inspection the new taxon will be colored accordingly. Example colors can
    be found [`here`](https://amoeba.msstate.edu/phylofisher/pdfs/svgcolors.pdf).

    <br>

2. Manual inspection of homolog trees.

    To manually inspect a homolog tree open the application `Parasorter` which can be downloaded from the PhyloFisher GitHub repository.

    Once ParaSorter has opened:

    1.  In the upper left corner click “Open tree” and choose an svg file created by forest.py in the last step.

    2. Click “Import tsv” and choose the corresponding gene’s tsv file


    To the right of each sequence in the single gene tree displayed there are three boxes (Figure 4). If
    selected, the leftmost box (green in color) will display a capital letter “O” for “ortholog”, the middle
    box (yellow in color) will display a capital letter “P” for “paralog”, and the rightmost box (red in color)
    will display a capital letter “D” for “delete.” These boxes are used to display and change a sequence’s
    current or future designation in the database. To change a sequences designation simply click the box that corresponds
    to the desired assignment. These designations will be applied to the starting database in the next step.


    Information provided in sequence headers (phylogenetic tree leaves) and single gene tree files to better inform ortholog, paralog, and contamination selection during visual inspection (Figure 4):
    
    - Full genus and species name of taxon

    - Route through `fisher.py` that produced sequence:

        - Specific Best Hit (SBH) – appended if a specific query produced a significant hit and the sequence WAS sister to a sequence within the database of the same taxonomy during FastTree analysis performed automatically by `fisher.py`

        - Best Blast Hit (BBH) - appended if a specific query produced a significant hit and the sequence WAS NOT sister to a sequence within the database of the same taxonomy during FastTree analysis performed automatically by `fisher.py`

        - HMMER route (HMM) – appended if the sequence was selected by the default route using hmmer search
        
    - Priority in final set of collected sequences:

    - Denoted “qn” where “n” is an integer representing the sequence’s order of priority out of “n sequences collected in the initial search using the profile HMMs (ex. q1, q2 . . ., qn).

    - If the collected sequence’s best BLAST hit is or is not a sequence in the corresponding ortholog alignment from the database.

        - c - collected sequence’s best BLAST hit IS a sequence in the corresponding ortholog alignment from the database.

        - n - collected sequence’s best BLAST hit IS NOT a sequence in the corresponding ortholog alignment from the database.

    - Proportional length of the sequence in the trimmed alignment used for length filtering

    - Short name of taxon in dataset

    - Higher and Lower taxonomic designations

    - Other important information provided:

        - Displayed at the top of each tree is the name of the gene, the length of trimmed alignment used to filter sequences, the length of the alignment used to produce the tree and the number of “suspicious clades” detected.

            - A clade is marked as suspicious if it is supported by a maximum likelihood bootstrap value of 70 or greater and contains sequences of mixed higher taxonomy. These clades are highlighted with a grey background and each node that meets the above criteria is marked with a red sphere.

        - Newly added sequences that were chosen as the putative ortholog by fisher.py are written in bold black font while sequences chosen as paralogs are written in regular black font.

        - Sequences that are newly added are not highlighted in color based on taxonomy. 

        - Orthologs already in the database are highlighted in color based on taxonomy and are written in regular black font.

        - Paralogs already in the database are not highlighted in color based on taxonomy and are written in regular blue font.

        - Sequences pre-marked for deletion are not highlighted in color based on taxonomy and are written in regular red font. Only present if known contaminants were provided to `forest.py` via the contaminants and backpropagate flags.

        <br><br>
        <figure>
            <img
            src="https://thebrownlab.github.io/phylofisher-pages/assets/images/Parasorter_display.jpg"
                height="75%"
                    width="100%" 
                    class="center"/>
                <figcaption>
                    Figure 4: Figure 4: Example and explanation of a single gene tree visualized with ParaSorter (above) and of the PhyloFisher sequence header naming scheme (below).
                </figcaption>
        </figure>       



    3. After all decisions have been made click “Save to tsv” on the top left-hand side of the `Parasorter` display. The default name `ParaSorter` will suggest for the new file will be {gene_name}_parsed.tsv. The file must have “{gene_name}_parsed.tsv” naming convention for subsequent steps of the workflow to perform correctly.

<br>

3. Tree parsing strategy used in creation of the PhyloFisher v.1.0 provided database.

    Below are the rules used in the creation of the PhyloFisher v.1.0 provided sequence database as described in Salomaki et al. 2020 and Tice et al. 2020. These rules are not immutable and in fact were a compromise between the authors. A user can choose to follow them or not. These are simply suggestion to help guide a user's ortholog selection decisions during this arduous portion of the workflow.

    1. In cases of in-paralogy, instances of a duplication event occuring in a single organism, the longest sequence was retained as the ortholog.

    2. In cases of mid or deep paralogy, clades with 50% or greater maximum likelihood bootstrap support and sequences from and least one taxon  present on both sides of the initial bifurcation were considered to represent gene duplication events.

        1. In the case of duplication events, sequences on the side of the duplication that contained the most sequence data (measured as the sum total of retained sequence length) were retained as the orthologs.

        2. In instances where the sequence data retention was nearly equal on both sides of the bifurcation, sequences from the side which had the most species represented retained as the orthologs.