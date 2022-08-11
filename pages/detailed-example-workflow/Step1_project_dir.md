---
layout: default
title: Project Directory Setup
parent: Detailed Example Workflow
nav_order: 1
permalink: /detailed-example-workflow/step1-project-dir
---
# Project Directory Setup

1. Make a project directory (named anything) in your desired location (this location can be anywhere on your computer and is independent of the location of the database).

    `mkdir <my_project_directory>`

2. Move into the new project directory:

    `cd <my_project_directory>`

3. Create an input_metadata.tsv file using information about your input data. See **Table 1** for an example. The input_metadata.tsv file contains nine required columns (detailed below) of information about input data. Each row in the file should be a new taxon to be added to the database. The input_metadata.tsv file can be most easily completed in a spreadsheet software such as Microsoft Excel and saved as a tab delimited text file. Place the completed input_metadata.tsv file in your project directory created in the previous step. After completion of a PhyloFisher run, the information in input_metadata.tsv will be appended to the permanent archival file “metadata.tsv” for any input taxon that is to be permanently added to the database.

    *  input_metadata.tsv is a tab separated file with nine required columns (detailed below and in **Table 1**)

        1. Location - the absolute path to the directory where the input proteome(s) are located.

        2. File Name - the name of the input proteome file.

        3. Unique ID - an abbreviated name for the input taxon (we have followed an eight-letter convention in the provided database but any number of characters may be used. **However, Unique IDs cannot contain underscores “_”, at symbols “@”, double dots “..”, white space, or asterisk “*” (with one exception outlined below).**

        4. Higher Taxonomy - The highest taxonomic rank for the input organism desired. We have chosen to use the “supergroup” level here but any user defined rank is accepted. However, we do recommend users choose a highly inclusive taxonomic rank here (phylum or class level in Linnaean terms) to promote the best possible performance of the fisher algorithm and other downstream tools.

        5. Lower Taxonomy - a taxonomic rank above the genus level for the input taxon.

             * NOTES ON TAXONOMY: Aspects of the PhyloFisher workflow require that taxonomic terms for both categories provided in “input_metadata.tsv” be the same as in the permanent archival file “metadata.tsv”. The only exception occurs when adding an organism with a taxonomic affiliation not represented in the database (see below). The default taxonomic terms in “metadata.tsv ” can be replaced with user preferred terms. If terms are to be replaced though, we recommend replacing them with synonyms of similar rank. **DO NOT MIX SYNONYMOUS TERMS (see example below)**. This will lead to misbehavior in the fisher algorithm and wrongly denoted suspicious clades during manual inspection of single gene trees. The same erratic behavior will likely occur if our chosen taxonomic ranks are split up and replaced by several less inclusive taxonomic terms.

            * New taxonomic terms) If you are adding an organism with a taxonomic affiliation of one or both taxonomic categories not already represented in the database, add an “\*” at the end (no space) of the unrepresented name in input_metadata.tsv to avoid a warning from fisher.py alerting you that the taxonomy is not in metadata.txt. If higher and lower taxonomy are unknown at the time of addition simply use some unique placeholder until proper taxonomic terms can be assigned later. **DO NOT USE TERMS YOU MAY REUSE LATER** such as “unknown” or “new. Failure to change out a term and then reusing it again later for an unrelated organism will cause erratic behavior in fisher.py and forest.py.

            * Example Taxonomic Change: If the term “Chromist” is preferred over “Stramenopiles” replace all instances of “Stramenopiles” in metadata.tsv with “Chromist” before adding new taxa with “Chromist” chosen as the higher taxonomic term in input_metadata.tsv **DO NOT MIX THE TWO** erratic behavior will ensue.

        6. Blast Seed - If the word ‘none’ is provided the ortholog fishing algorithm will proceed through the default route. If the algorithm is to proceed through the phylogenetically aware route at least one Unique ID of a related organism already in the database must be provided. Use explore_database.py or open metadata.tsv to get a list of all Unique IDs of taxa already present in the provided database. There is no limit to the number of Unique IDs that can be provided here. Unique IDs of taxa must be separated by only a comma with no space in between.

        7. Long Name - Full name of the input taxon. The long name cannot cannot contain underscores “_”, at symbols “@”, double dots “..”.

        8. Data Type - A place to add a note about the type of data being added (ex.transcriptomic, genomic, EST . . .)

        9. Source - A place to add notes about the source of the data such as accession numbers, “in-house information”, strain information etc. If a delimiter is needed here we recommend pipe ”\|”.

        <br>
        <br>
    
    | Location |   File Name  | Unique ID | Higher Taxonomy | Lower Taxonomy |    BLAST Seed    |      Long Name      |    Data Type   | Source |
    |:--------:|:------------:|:---------:|:---------------:|:--------------:|:----------------:|:-------------------:|:--------------:|:------:|
    |  toAdd/  | Cuneruss.faa |  Cuneruss |    Amoebozoa    |    Discosea    | Acancas,Dictdisc |     Cunea russae    | Transcriptomic | SRR123 |
    |  toAdd/  | Mhelmari.faa |  Mhelmari |     Erebor*     |  Microhelida*  |       none       | Microheliella maris | Transcriptomic | SRR345 |

    **Table 1:** Example of “input_metadata.tsv”. Here two proteomes predicted from transcriptomic data for *Cunea russae* (Amoebozoa, Discosea) SRA accession SRR123 and *Microheliella maris* (Erebor, Microhelida) SRA accession SRR345 will be added to the database. Both predicted proteomes are located in the directory “toAdd/” within the project directory.  The proteomes will have the Unique IDs “Cunruss” and "Mhelmari" respectively. Orthologs in the starting dataset from *Acanthamoeba castellanii* (Unique ID=Acancast)and *Dictyostelium discoideum* (Unique ID=Dictdisc) will be used as queries in the BLAST searches against the *C*. *russae* predicted proteome. No BLAST queries from existing taxa in the database will be used to query the *M*. *maris* proteome. Since each taxonomic rank for *M*. *maris* does not already exist in the database an "*" is added at the end of each.
<br>
<br>
4. Create and set up the PhyloFisher configuration file.

    `config.py [OPTIONS] -d <path_to_database> -i <path_to_input_metadata.tsv>`
    <br>
    <br>

    Required arguments:

   - `-d`, `--database_folder <database_dir>` Path to database directory
    
   - `-i`, `--input_file <input.tsv>` Path to input_metadata.tsv
    <br>
    <br>
    
    Optional arguments:
   
   - `--orthomcl <omcl_data>` Path to orthomcl if not in default location
    
   - `--tree_colors <tree_colors.tsv>` Path to alternative single gene tree color configuration file

    - `-h`, `--help` Show this help message and exit
    <br>
    <br>

    Default config.py output:

     * a file called “config.ini” that contains the paths specified in input.
