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

    - `-t`, `--threads <N>` Total number of cores/threads Snakemake may use to run jobs in parallel. Ignored when `--profile` is given.
        - Default: 1
    - `--threads-per-job <N>` Number of threads each individual tool run (MAFFT, RAxML-ng) should use
        - Default: 1
    - `-if`, `--in_format <format>` Format of input files
        - Options: `fasta`, `phylip`, `phylip-relaxed`, or `nexus`
        - Default: `fasta`
    - `--no_trees` Do not build single gene trees. Length filtration and trimming only.

    - `--trees_only` Only build single gene trees. No length filtration or trimming is performed.

    - `--length_filter_only` Only perform length filtration. No final alignment, trimming, or tree building.

    - `--profile <profile>` Snakemake profile to use for submitting jobs (e.g., to a cluster scheduler such as SLURM)
        - Default: None

    - `-n`, `--dry-run` Perform a dry run of the Snakemake workflow without executing any jobs

    - `-o`, `--output <out_dir>` Path to user-defined output directory
        - Default: `./sgt_constructor_out_<M.D.Y>`

    - `-h`, `--help` Show this help message and exit

    Default `sgt_constructor.py` output:

    - a directory `sgt_constructor_out_<M.D.Y>` that contains:
    
        - a directory `prequal` that contains the files:
        
            - `{gene_name}.aa` - unaligned gene file used as PREQUAL input

            - `{gene_name}.aa.filtered` - PREQUAL filtered sequence file used as input for MAFFT in the length filtration step

            - `{gene_name}.aa.filtered.PP` - output of PREQUAL ##

            - `{gene_name}.aa.warning` - output of PREQUAL ##

        - a directory `length_filter_mafft` that contains the file:

            - `{gene_name}.aln` - aligned gene file in fasta format used as input for Divvier during length filtration

        - a directory `length_filter_divvier` that contains the files:

            - `{gene_name}.aln.partial.fas` - Divvier filtered alignment $$

            - `{gene_name}.aln.PP` - output of Divvier $$

        - a directory `length_filter_bmge` that contains the files:

            - `{gene_name}.pre_bmge` - modified version of `{gene_name}.aln.partial.fas` with the character “X” replaced by the character “-” used as input for BMGE

            - `{gene_name}.bmge` - output of BMGE, used to calculate the coverage of each sequence during length filtration

        - a directory `length_filtered` that contains the file:

            - `{gene_name}.length_filtered` - unaligned PREQUAL filtered sequences that passed length filtration, used as input for the second run of MAFFT. This file is empty if every sequence was removed, in which case the gene is skipped by all subsequent steps.

        - a directory `mafft` that contains the file:

            - `{gene_name}.aln` - output of the second run of MAFFT and input for the second run of Divvier

        - a directory `divvier` that contains the files:

            - `{gene_name}.aln.partial.fas` - output of the second run of Divvier and input for trimAl $$

            - `{gene_name}.aln.PP` - output of Divvier $$

        - a directory `trimal` that contains the files:

            - `{gene_name}.trimal` - output of trimAl

            - `{gene_name}.final` - trimmed alignment with sequences that contain no residues removed. Input for RAxML-ng

        - a directory `raxml` that contains the files:

            - `{gene_name}.raxml.rba` &&

            - `{gene_name}.raxml.startTree` &&

            - `{gene_name}.raxml.bestTree` &&

            - `{gene_name}.raxml.mlTrees` &&

            - `{gene_name}.raxml.support` &&

            - `{gene_name}.raxml.bestModel` &&

            - `{gene_name}.raxml.bootstraps` &&

            - `{gene_name}.raxml.log` &&

        - a directory `done` that contains an empty `{gene_name}.done` file marking each gene that has completed the workflow

        - a directory `logs` that contains:

            - a directory `prequal` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through PREQUAL

            - a directory `length_filter_mafft` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through the MAFFT step of length filtration

            - a directory `length_filter_divvier` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through the Divvier step of length filtration
            
            - a directory `x_to_dash` that contains the files:
                
                - `{gene_name}.log` - the log file for each gene run through replacement of X’s, as part of length filtration

            - a directory `length_filter_bmge` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through the BMGE step of length filtration

            - a directory `length_filtered` that contains the files:
        
                - `{gene_name}.log` - the log file for the length filtration of each gene, listing every sequence removed and its coverage

            - a directory `mafft` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through MAFFT

            - a directory `divvier` that contains the files:

                 - `{gene_name}.log` - the log file for each gene run through Divvier

            -  a directory `trimal` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through trimAl
                
            - a directory `raxml` that contains the files:

                - `{gene_name}.log` - the log file for each gene run through RAxML-ng

            - `tar_local_dir.log` - the log file for the creation of `sgt_constructor_out_<M.D.Y>-local.tar.gz`

        - a directory `trees` that contains:

            - `{gene_name}.trimmed` - the BMGE trimmed alignment used for length filtration of each gene

            - `{gene_name}.final` - the trimmed alignment file used for tree construction by RAxML-ng

            - `{gene_name}.treefile` - the final ML tree with bootstrap support values for each gene (a copy of `{gene_name}.raxml.support`)

    - a file `sgt_constructor_out_<M.D.Y>-local.tar.gz` - a compressed archive of a directory `sgt_constructor_out_<M.D.Y>-local` (the uncompressed directory is removed once the archive is created). This archive eases the movement of all required data over to a local machine to render the svg files used in the next step. This is often necessary due to the lack of graphics capabilities of headless servers. The archive contains:

        - a directory `trees` that contains: 

            - `{gene_name}.trimmed` - the BMGE trimmed alignment used for length filtration of each gene

            - `{gene_name}.untrimmed` - the untrimmed MAFFT alignment of each gene (from the `mafft` directory)

            - `{gene_name}.final` - the trimmed alignment file used for tree construction by RAxML-ng

            - `{gene_name}.treefile` - the final ML tree with bootstrap support values for each gene

        - `metadata.tsv` - the file that contains information about taxa already in the database

        - `input_metadata.tsv` - the input file that contains information about newly added taxa

        - `tree_colors.tsv` - the file used by `forest.py` in the next step to color taxa by taxonomic affiliation

    When `--length_filter_only` is used, the workflow stops after length filtration and instead writes a file `sgt_constructor_out_<M.D.Y>-length_filtered.tar.gz`, a compressed archive of the `length_filtered` directory.

    When `--no_trees` is used, the workflow stops after trimAl and no `raxml` or `trees` directories or `-local.tar.gz` archive are produced.

    When `--trees_only` is used, trees are built directly from the input files, and the `trees` directory and `-local.tar.gz` archive contain only the `{gene_name}.final` (a copy of the input alignment) and `{gene_name}.treefile` files.

\## - These are standard PREQUAL output files for each gene that PhyloFisher has appended
the corresponding gene name to. See the [`PREQUAL documentation`](https://amoeba.msstate.edu/phylofisher/pdfs/prequal.pdf) for a thorough explanation
of their contents.

\$$ - These are standard Divvier output files for each gene that PhyloFisher has appended the
corresponding gene name to. See the [`Divvier documentation`](https://amoeba.msstate.edu/phylofisher/pdfs/divvier.pdf) for a thorough explanation of their
contents.

&& - These are standard RAxML-ng output files for each gene that PhyloFisher has appended the corresponding gene name to. See the [`RAxML-ng documentation`](https://github.com/amkozlov/raxml-ng/wiki) for a thorough explanation of their contents.

**NOTE:** For a detailed explanation of the methodology implemented in `sgt_constructor.py` see "Automated Filtering, Alignment, Trimming, and Gene Tree Construction."

**NOTE:** If `sgt_constructor.py` dies in the middle of a run, simply provide the `sgt_constructor_out_<M.D.Y>` output directory from the previous run to `sgt_constructor.py` via the `-o` flag in addition to the previous command and the script will pick up where it left off.

**NOTE:** If `sgt_constructor.py` is submitted to a compute node without internet access, the creation of internal conda environments will fail. To circumvent this, run `sgt_constructor.py` from the command line on the head node until the conda environments are created. Then kill the process and submit `sgt_constructor.py` to a compute node.

**NOTE:** Rather than running every job on a single machine, `sgt_constructor.py` can submit each job to a cluster scheduler (e.g., SLURM) via a [Snakemake profile](https://snakemake.readthedocs.io/en/stable/executing/cli.html#profiles) passed to `--profile`. When a profile is given, the number of concurrent jobs is controlled by the profile rather than `-t`. Use `-n`/`--dry-run` to preview the jobs that would be run.

**NOTE:** If `sgt_constructor.py` is circumnavigated to use alternative parameters for sequence filtering, alignment, and tree reconstruction the following criteria must be met to renter the workflow and downstream steps perform correctly:

- Trees must have been built using a maximum likelihood program.  Downstream quality control steps are not set up to interpret Bayesian
posterior probability values.

- The directory structure of `sgt_constructor_out_<M.D.Y>-local` outlined above must be replicated.  To do this

    1. Make a directory `my_directory` and within `my_directory` directory make a subdirectory called `trees`.

    2. Tree files must be in Newick format, follow the naming convention `{gene_name}.treefile`, and be located in the `trees` subdirectory. (Trees named `{gene_name}.raxml.support`, as produced by PhyloFisher versions prior to v1.3.0, are also accepted.)

    3. Sequence files used to build the trees must follow the naming convention `{gene_name}.final` and be located in the `trees` subdirectory.

    4. Sequence files used for length filtering must follow the naming convention `{gene_name}.trimmed` and be located in the `trees` subdirectory. THESE FILES ARE OPTIONAL.

    5. The files `metadata.tsv` and `tree_colors.tsv` can be copied from `PhyloFisherDatabase_v1.0/database/` and placed into `my_directory` along with the `input_metadata.tsv` file.
