---
layout: default
title: Quickstart
parent: Getting Started
nav_order: 4
permalink: /getting-started/quickstart/
---

# Quickstart

1. Make a project directory (named anything) and move into it <br/>
    `mkdir <project_directory>`<br/>
    `cd <project_directory> ` 

2. `explore_database.py`
    * Explore the contents of PhyloFisher’s provided starting database (found here: https://ndownloader.figshare.com/files/29093409) to help make decisions on proteomes to add (Optional)
    * Usage: `explore_database.py [OPTIONS]`
    
3. Fill out `input_metadata.tsv`
    * Each proteome to be added to the database should be included 
    * See Table 1 for an example and detailed explanation of `input_metadata.tsv`
      
4. `config.py`
    * `config.py` allows users to configure the analysis directory
    * Usage: `config.py [OPTIONS] -d <database_folder> -i <input_file.tsv>`
    
5. `fisher.py`
    * Run `fisher.py` for homolog collection.
    - Usage: `fisher.py [OPTIONS]`
    
6. `informant.py`
    * Prepare preliminary statistics for and select organisms and genes prior to homolog tree construction
    * Usage: `informant.py [OPTIONS] -i <fisher_out_dir>`<br/>
    
7. `working_dataset_constructor.py`
    * Apply your selections from the previous step
    * Usage: `working_dataset_constructor.py [OPTIONS] -i <fisher_out_dir>`

8. `sgt_constructor.py`
    * Length filtration, trimming, and homolog tree construction
    * Usage: `sgt_constructor.py [OPTIONS] -i <working_dataset_constructor_out_dir>`
    
9. `forest.py`
    * Tree visualization.
    * Usage: `forest.py [OPTIONS] -i <dir_containing_tress>`
    
10. `apply_to_db.py`
    * Apply parsing decisions and add new data to the database:
    * Usage: `apply_to_db.py [OPTIONS] -i <forest_out_dir>`
    
11. `select_taxa.py` (OPTIONAL)
    * Select a subset of taxa from the database for final phylogenomic analyses.
    * Usage: `select_taxa.py [OPTIONS]`
    
12. `select_orthologs.py` (OPTIONAL)
    * Select a subset of orthologs from the database for final phylogenomic analyses.
    * Usage: `select_orthologs.py [OPTIONS]`
    
13. `prep_final_dataset.py`
    * Collect taxa and genes for final phylogenomic analyses.
    * Usage: `prep_final_dataset.py [OPTIONS]`
    
14. `matrix_constructor.py`
    * Build phylogenomic matrix (Concatenation).
    * Usage: `matrix_constructor.py [OPTIONS] -i <prep_final_dataset_out_dir>`<br/>
 

***Use `<script>.py --help`  to see all options and their descriptions.