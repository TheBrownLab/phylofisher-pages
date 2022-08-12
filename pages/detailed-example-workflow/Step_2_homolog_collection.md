---
layout: default
title: Homolog Collection
parent: Detailed Example Workflow
nav_order: 2
permalink: /detailed-example-workflow/step2-project-dir
---

# Homolog Collection

1.  Collect putative homologs from input taxa using `fisher.py`

    `fisher.py [OPTIONS]`

    Optional arguments: 
    - `-t`, `--threads <N>` Number of threads, where N is an integer
        - Default : 1

    - `-n`, `--max_hits <N>` Max number of hits to collect, where N is an integer

        - Default: 5

    - `--keep_tmp` Keep temporary files

    - `--all_BBH`  Keep all significant BLAST hits regardless of phylogenetic affiliation as determined with FastTree through the phylogenetically aware route

    - `--add <input_metadata.tsv>` Path to input metadata file(different from original the one in config.ini) that contains new input proteomes. Must be used with –add_to option below.

     - `--add_to <fisher_out>` Previous fisher.py output directory to add to. Must be used with the `--add` option above.

     - `-o`, `--output <out_dir>` Path to user-defined output directory

        - Default: `./fisher_out_<M.D.Y>`
     - `-h`, `--help`  Show this message and exit.

    Default fisher.py output:

    * a directory called `fisher_out_<M.D.Y>` that contains:

        - fasta files of orthologs from the database with putative homologs  from newly input taxa appended to the end of the fasta file. NOTE: if no putative homologs were found in any newly input proteome for a particular ortholog in the database, that ortholog will not be present in this directory. All files will have the extension “.fas”.

        - a tab delimited file called “orgininal_names.tsv” with the original sequence headers from the input proteomes that were clustered by CD-HIT in fisher.py in the first column and a new “clean” name assigned by `fisher.py` made up of the chosen Unique ID and a numbered 1 to N.

    * a file “noncorresponding_hits.txt” that contains:

        - information regarding collected sequences whose best BLAST hit was not the corresponding ortholog in the database. (See fisher algorithm details for more information on this criterion). This file will NOT appear if the best BLAST hit of each retained sequence is the corresponding ortholog from the database.

    NOTE: Users that plan to collect homologs from more taxa prior to single gene tree construction should stop here for now.
<br>
<br>

2. Running more rounds of addition prior to single gene tree construction (OPTIONAL).


    `fisher.py [OPTIONS] --add <Add_More_Taxa.tsv> --add_to <previous_fisher_out_dir>`

    Use -–add option in combination with the --add_to option of `fisher.py` to include homologs from more taxa in another round of addition to the working dataset. Create a new file identical to input_metadata.tsv in structure except with a different name (Ex. Add_More_Taxa.tsv). Put this new file in the project directory created in STEP 1. The information in this new text file will be appended to input_metadata.tsv.


    NOTE: We recommend checking that the information contained in the new input file was added to the end of “input_metadata.tsv” after the new addition run is complete. If so, delete the new input file after addition is complete to avoid unnecessary clutter in the directory
<br>
<br>

3. Produce preliminary statistics about newly input data.

    `informant.py [OPTIONS] -i <input_directory>`

    Required arguments:

   - `-i`, `--input <input_dir>` Path to `fisher.py` output directory

    Optional arguments:
    
    - `--orthologs_only`    Paralogs will NOT be included from any taxa in the database in downstream single gene tree construction.

    - `-h`, `--help` Show this help message and exit

    At this step the statistics provided by informant.py should be considered preliminary. The number of orthologs shown for a newly input taxon can be inflated due to contamination in the data or if fisher.py harvested only a paralog for a particular gene (If only one sequence passes all criteria it is automatically marked the putative ortholog but is not always the true ortholog). These statistics will almost always change after manual curation. However, they can be generated quickly and are useful for a rough estimate of data quality.

    Default `informant.py` output (found in the fisher.py output directory provided to `informant.py` via the `-i`, `--input` options):

    -  directory called `informant_stats` that contains five files:
    
        - db_taxa_stats.tsv - a comma separated file with taxa as rows and seven columns:
            
            1. Unique ID - short name of organism in the database
            2. Long Name - full name of organism in the database
            3. Higher Taxonomy - highest taxonomic level assigned to the taxon in metadata.tsv
            4. Lower Taxonomy - lower taxonomic level assigned to the taxon in metadata.tsv
            5. Genes collected out of “N”- number of genes present in taxa already in the database where N is the number of genes found by `fisher.py` for all newly added taxa
            6. SGT - will allow for the inclusion (YES) or exclusion (NO) of taxa in single gene tree construction on a per taxon basis
            7. Paralogs - will allow for the inclusion (YES) or exclusion (NO) of paralogs on a per taxon basis for single gene tree construction. If no paralogs exist for an organism in the database this column will be labelled “none”. If the `--orthologs_only` flag was used, columns for all taxa that have paralogs in the database will be marked “NO.”

        - genes_stats.tsv - a comma separated file with gene names from the database as rows
        and four columns. Only genes that had a sequence from at least one newly added taxon appended to the alignment are included.

            1. Gene Name - gene name in the database
            2. Number of Taxa - number of taxa which the gene is present
            3. Percent of Total Taxa (out of “N”) - percentage of taxa which have the gene where N is the total number of taxa.
            4. SGT - include gene in gene tree construction step. To be used by `working_dataset_constructor.py` downstream
        
        - new_taxa_stats.tsv - a comma separated file with taxa as rows and ten columns:

            1. Unique ID - short name of organism in the database
            2. Long Name - full name of organism in the database
            3. Higher Taxonomy - highest taxonomic level assigned to the taxon in metadata.tsv
            4. Lower Taxonomy - lower taxonomic level assigned to the taxon in metadata.tsv
            5. Genes collected out of “N”- number of genes present in newly added taxa where N is the number of genes found by `fisher.py` for all newly added taxa
            6. Sequences collected - number of total sequences collected by `fisher.py` for a taxon.
            7. #SBH - number of collected sequences for a taxon where the specific query used produced a significant hit from the input proteome and the collected sequence WAS sister to a sequence already present in the database of the same Higher Taxonomy during FastTree analysis performed automatically by `fisher.py`
            8. #BBH - number of collected sequences for a taxon where the specific query used produced a significant hit and the collected sequence WAS NOT sister to a sequence already present in the database of the same higher taxonomy during FastTree analysis performed automatically by `fisher.py`
            9. #HMM - number of collected sequences for a taxon that were selected by the default HMM route.
            10. SGT - will allow for the inclusion (YES) or exclusion (NO) of taxa in gene tree construction on a per taxon basis

        – occupancy.tsv - a comma separated file with taxa as rows and genes in the starting dataset as columns. A “0” (zero) indicates a gene is absent in a taxon. Any non-zero number is the number of sequences collected for that “gene” for a taxon.

        – occupancy_with_routes.tsv - a comma separated file with taxa as rows and genes in the non-zero number is the number of sequences collected for that “gene” for a taxon. The abbreviation for the route through `fisher.py` that each gene was collected (either SBH,BBH, HMM) by is appended to
    <br>
    <br>

4. Collect taxa, and homologs for gene tree construction

    `working_dataset_constructor.py [OPTIONS] -i <input_directory>`

    Required arguments:

    `-i`, `--input <input_dir>` Path to output directory of `fisher.py` that contains the output of `informant.py`

    Optional arguments:
    
   - `-o`, `--output <out_dir>` Path to user-defined output directory
    
        - Default: `./working_dataset_constructor_out_<M.D.Y>`
    
    - `-h`, `--help` Show this help message and exit

    NOTE: To exclude genes, newly added taxa, or taxa already in the database, from the working dataset used for gene tree construction (NOT RECOMMENDED) change the column values for the column “SGT” in gene_stats.tsv new_taxa_stats, db_taxa_stats.tsv respectively to “NO.” To exclude previously identified paralogs for taxa change the value for "Paralogs" in db_taxa_stats.tsv to "NO." 

    Default `working_dataset_constructor.py` output:

      - A directory `working_dataset_constructor_output_<M.D.Y>` that contains:

        - fasta files of genes to be included in single gene tree construction. This will be either all or the chosen subset of the gene files contained in the input directory. Each gene file contains only taxa to be included in single gene tree construction.