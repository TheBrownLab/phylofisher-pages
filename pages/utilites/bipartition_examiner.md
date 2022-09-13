---
layout: default
title: bipartition_examiner.py
parent: Utilities
nav_order: 4
permalink: /utilities/bipartition-examiner
---

# `bipartition_examiner.py`

Calculate and plot the observed occurrences of clades of interest in bootstrap trees.

`bipartition_examiner.py [OPTIONS] -b <input_MLBS_files> -g groups.txt`

Required arguments:
- `-b`, `--bs_files <infile>` A file that contains paths to sets of bootstrap tree files. One file name per line (Table 5). Results from files will be plotted in the order they were provided
- `-g`, `--groups <infile>` A file containing taxonomic groups/relationships of interest one per line (Table 6)

Optional arguments:
- `--database` Path to database if not using config.ini
- `--chimeras` A .tsv containing a Unique ID, higher taxonomy, and lower taxonomy for each chimera within the input bootstrap files. The file contains three columns:
  - Chimera_ID 1
  - Higher_Tax
  - Lower_Tax
- `--bar_plot` Plot categorical data as a barplot
  - Default: Plot series data as a line graph.
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./bipartition_examiner_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit.

`bipartion_examiner.py` output:
- `bipartion_examiner.pdf` - a plot (line graph or histogram) with MLBS values on the y-axis file names on the x-axis. Groups of interest are color coded.
- `bipartion_examiner.tsv` - a .tsv file that contains the values plotted in `bipartion_examiner.pdf`

<br><br>
<figure>
    <table class="center">
        <tr>
            <td>/home/myworkingdirectory/MLbootstrap.experiment1</td>
        </tr>
        <tr>
            <td>/home/myworkingdirectory/MLbootstrap.experiment2</td>
        </tr>
        <tr>
            <td>/home/myworkingdirectory/MLbootstrap.experiment3</td>
        </tr>
    </table>
        <figcaption>
            Example input file provided to bipartition_examiner.py via the -b/--bs_files options providing the location of input sets of bootstrap trees. The results will be plotted in the order the files were provided.
        </figcaption>
</figure>

<br><br>
<figure>
    <table class="center">
        <tr>
            <td>Amoebozoa</td>
        </tr>
        <tr>
            <td>Amoebozoa+Obazoa+CRuMs</td>
        </tr>
        <tr>
            <td>Fungi+Metazoa</td>
        </tr>
        <tr>
            <td>Homosapi+Gallgall</td>
        </tr>
        <tr>
            <td>Fungi:Sacccere,Candalbi,Aspefumi,Coprcine</td>
        </tr>
    </table>
     <figcaption>
            Example input file provided to bipartition_examiner.py via the -g/--groups options that lists the groups of interest to be examined in the sets of bootstrap trees. If the data has been processed through the PhyloFisher workflow and a metadata.tsv exists detailing the higher and lower taxonomy of each taxon in the dataset then these taxonomic terms can be utilized here along with individual Unique IDs to examine support for relationships of interest. In summary, lines 1-4 are only if the data has been processed through the PF workflow and a metadata file exists. If bipartion_examiner.py is being used as a stand-alone tool each group of interest will have to be defined as in line 5. Here the group label (Fungi) is followed by a colon and sequence headers (ex. Sacccere) of all taxa in the group are listed and separated by commas.
        </figcaption>
</figure>
