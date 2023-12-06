---
layout: default
title: Gene Tree Construction
parent: Detailed Example Workflow
nav_order: 3
permalink: /detailed-example-workflow/step3-project-dir
---

# Filter, align, and trim  gene files followed by gene tree construction

1. Construct gene trees:

    `sgt_constructor.py [OPTIONS] -i <input_directory>`

    Required arguments:

    - `-i`, `--input <input_dir>` Path to output of `working_dataset_constructor.py`

    Optional arguments:

    - `-t`, `--threads <N>` Number of threads
        - Default: 1
    - `--no_trees` Do not build single gene trees

    - `--trees_only <in_dir>` Only build single gene trees. No other operations performed

    - `-o`, `--output <out_dir>` Path to user-defined output directory
        - Default: `./sgt_constructor_out_<M.D.Y>`

    - `-h`, `--help` Show this help message and exit

    Default `sgt_constructor.py` output:

    - a directory `sgt_constructor_out_<M.D.Y>` that contains:
    
        - a directory `prequal` that contains the files:
        
            - `{gene_name}.aa` - unaligned gene file used as PREQUAL input

            - `{gene_name}.aa.filtered` - PREQUAL filtered sequence file used as input for MAFFT in subsequent length filtration step

            - `{gene_name}.aa.filtered.PP` - output of PREQUAL ##

            - `{gene_name}.aa.warning` - output of PREQUAL ##

        - a directory `length_filtration` that contains:

            - a directory `mafft` that contains the file:

                - `{gene_name}.aln` -  aligned gene file in fasta format used as input for Divvier

            - a directory `divvier` that contains the files:

                - `{gene_name}.aln.divvy.fas` - Divvier filtered sequence file $$

                - `{gene_name}.aln.PP` - output of Divvier $$

            - a directory `BMGE` that contains the files:

                - `{gene_name}.pre_bmge` - modified version of “gene_name.aln.divvy.fas” with the character “X” replaced by the character “-” used as input for BMGE

                - `{gene_name}.bmge` - output of BMGE and input for the length filtration step
            
                - `{gene_name}.length_filtered` - length filtered fasta file used as input for a second run of MAFFT

             - a directory `mafft` that contains the file:

                – `{gene_name}.aln2` - output of the second run of MAFFT and input for a second run of Divvier

        - a directory `divvier` that contains the files:

            - `{gene_name}.aln2.divvy.fas` - output of the second run of Divvier and input for timAl

             - `{gene_name}.aln2.PP` - output of Divvier $$

        - a directory `trimAl` that contains the files:

            - `{gene_name}.final` - trimmed alignment in fasta format and input for RAxML
            
            - `{gene_name}.final.reduced` - trimmed alignment in phylip format

        - a directory `RAxML` that contains the files:

            - `{gene_name}.raxml.bestTreeCollapsed` &&

            - `{gene_name}.raxml.rba` &&

            - `{gene_name}.raxml.startTree` &&

            - `{gene_name}.raxml.bestTree` &&

            - `{gene_name}.raxml.mlTrees` &&

            - `{gene_name}.raxml.support` &&

            - `{gene_name}.raxml.bestModel` &&

            - `{gene_name}.raxml.bootstraps` &&

            - `{gene_name}.raxml.log` &&

            
        - a directory `logs` that contains:

            - a directory `prequal` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through PREQUAL

            - a directory `length_filter_mafft` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through the MAFFT step of length filtration

            - a directory `length_filter_divvier` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through the Divvier step of length filtration
            
            - a directory `x_to_dash` that contains the files:
                
                - `{gene_name}.log` - the log file for each gene run through removal of X’s from gene files, as part of length filtration

            - a directory `length_filter_bmge` that contains the files:

                - `{gene_name}.log` - the log file for gene run through BMGE step of length filtration

            - a directory `length_filtration` that contains the  files:
        
                - `{gene_name}.log` - the log file for the length filtration of gene

            - a directory `mafft` that contains the files:

                - `{gene_name}.log` - the log file for gene run through MAFFT

            - a directory `divvier` that contains the files:

                 - `{gene_name}.log` - the log file for gene run through Divvier

            -  a directory `trimal` that contains the files:

                - `{gene_name}.log` - the log file for gene run through trimAL
                
            - a directory `raxml` that contains the files:

                - `{gene_name}.log` - the log file for gene run through RAxML

        - a directory `trees` that contains:

            - `{gene_name}.trimmed` - the trimmed alignment file used for length filtration of each gene

            - `{gene_name}.final` - the trimmed alignment file used for tree construction by RAxML

            - `RAxML_bipartitions.{gene_name.tre}` - the final bootstrapped ML tree for each gene

    - a directory `sgt_constructor_out_<M.D.Y>-local` that contains:

        - a directory `trees` that contains: 

            - `{gene_name}.trimmed` - the trimmed alignment file used for length filtration of each gene

            - `{gene_name}.final` - the trimmed alignment file used for tree construction by RAxML

            - `RAxML_bipartitions.{gene_name}.tre` - the final bootstrapped ML tree for each gene

        - `metadata.tsv` - the file that contains information about taxa already in the database

        - `input_metadata.tsv` - the input file that contains information about newly added taxa

        - `tree_colors.tsv` - the file used by `forest.py` in the next step to color taxa by taxonomic affiliation

    - a file `sgt_constructor_out_<M.D.Y>.tar.gz` - a compressed file of the directory `sgt_constructor_out_<M.D.Y>-local` created to ease the movement of all required data over to a local machine to render the svg files used in the next step. This is often necessary due to the lack of graphics capabilities of headless servers.

\## - These are standard PREQUAL output files for each gene that PhyloFisher has appended
the corresponding gene name to. See the [`PREQUAL documentation`](https://amoeba.msstate.edu/phylofisher/pdfs/prequal.pdf) for a thorough explanation
of their contents.

\$$ - These are standard Divvier output files for each gene that PhyloFisher has appended the
corresponding gene name to. See the [`Divvier documentation`](https://amoeba.msstate.edu/phylofisher/pdfs/divvier.pdf) for a thorough explanation of their
contents.

&& - These are standard RAxML-ng output files for each gene that PhyloFisher has appended the corresponding gene name to. See the [`RAxML-ng documentation`](https://github.com/amkozlov/raxml-ng/wiki) for a thorough explanation of their contents.

NOTE: For a detailed explanation of the methodology implemented in `sgt_constructor.py` see "Automated Filtering, Alignment, Trimming, and Gene Tree Construction."

NOTE: If `sgt_constructor.py` dies in the middle of a run, simply provide the `sgt_constructor_out_<M.D.Y>` output directory from the previous run to `sgt_constructor.py` via the `-o` flag in addition to the previous command and the script will pick up where it left off.

NOTE: If `sgt_constructor.py` is circumnavigated to use alternative parameters for sequence filtering, alignment, and tree reconstruction the following criteria must be met to renter the workflow and downstream steps perform correctly:

NOTE: If `sgt_constructor.py` is submitted to a compute node without internet access, the creation of internal conda environments will fail. To circumvent this, run `sgt_constructor.py` from the command line on the head node until the conda environments are created. Then kill the process and submit `sgt_constructor.py` to a compute node.

- Trees must have been built using a maximum likelihood program.  Downstream quality control steps are not set up to interpret Bayesian
posterior probability values.

- The directory structure of `sgt_constructor_out_<M.D.Y>-local` outlined above must be replicated.  To do this

    1. Make a directory `my_directory` and within `my_directory` directory make a subdirectory called `trees`.

    2. Tree files must follow the naming convention `{nameofchoosing}.{gene_name}.tre` and be located in the `trees` subdirectory.

    3. Sequence files used to build the trees must follow the naming convention `{gene_name}.final` and be located in the `trees` subdirectory.

    4. Sequence files used for length filtering must follow the naming convention `{gene_named}.trimmed` and be located in the `trees` subdirectory. THESE FILES ARE OPTIONAL.

    5. The files `metadata.tsv` and `tree_colors.tsv` can be copied from `PhyloFisherDatabase_v1.0/database/` and placed into `my_directory` along with the `input_metadata.tsv` file.

